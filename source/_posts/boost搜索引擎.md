---
title: boost搜索引擎
date: 2025-05-14 13:48:35
categories: 
  - "编程实战"
tags:
  - "Boost" 
  - "服务器"
description: |
    基于boost官方文档制作的搜索引擎
---


# 宏观原理
客户通过http的GET请求，上传搜索关键字，进行搜索。
服务器在搜索模块，通过检索索引得到相关的html，（去标签&&数据清理，建立索引）
拼接多个网页的title和desc+url，构建成html返回给用户。

# 用到的技术
c/c++,STL,准标准库Boost,Jsoncpp,cppjieba,cpp-httplib

# 正排索引和倒排索引
正派索引，就是建立文档ID和文档内容的关系，通过文档ID搜索文档内容
倒排索引，就是建立文档内容（分词）和文档ID的关系，通过文档内容搜索文档ID（需要先分词）



# 数据区标签和数据清洗的模块Parser



```cpp
#include<iostream>
#include<string>
#include<vector>
#include<boost/filesystem.hpp>
#include<util.hpp>

const std::string src_path="/boost_searcher/data/input";
const std::string output="data/raw_html/raw.txt";

typedef struct DocInfo{
    std::string title;   //文档的标题
    std::string content; //文档内容
    std::string url;     //该文档在官网中的url
}DocInfo_t;

bool EnumFile(const std::string &src_path,std::vector<std::string> *files_list);
bool ParseHtml(const std::vector<std::string>&files_list,std::vector<DocInfo>* results);
bool SaveHtml(std::vector<DocInfo> &results,const std::string &output);
int main()
{
    std::vector<std::string> files_list;
    //第一步: 递归式的把每个html文件名带路径，保存到files_list中，方便后期进行一个一个的文件进行读取
    if(!EnumFile(src_path, &files_list)){
        std::cerr << "enum file name error!" << std::endl;
        return 1;

    }
    //第二步: 按照files_list读取每个文件的内容，并进行解析
    std::vector<DocInfo_t> results;
    if(!ParseHtml(files_list, &results)){
        std::cerr << "parse html error" << std::endl;
        return 2;
    }

    //第三步: 把解析完毕的各个文件内容，写入到output,按照\3作为每个文档的分割符
    if(!SaveHtml(results, output)){
        std::cerr << "sava html error" << std::endl;
        return 3;
    }

    return 0;
}

bool EnumFile(const std::string &src_path, std::vector<std::string> *files_list)
{
    namespace fs = boost::filesystem;
    fs::path root_path(src_path);

    //判断路径是否存在，不存在，就没有必要再往后走了
    if(!fs::exists(root_path)){
        std::cerr << src_path << " not exists" << std::endl;
        return false;
    }

    //定义一个空的迭代器，用来进行判断递归结束
    fs::recursive_directory_iterator end;
    for(fs::recursive_directory_iterator iter(root_path); iter != end; iter++){
        //判断文件是否是普通文件，html都是普通文件
        if(!fs::is_regular_file(*iter)){ 
            continue;
        }
        if(iter->path().extension() != ".html"){ //判断文件路径名的后缀是否符合要求
            continue;
        }
        //std::cout << "debug: " << iter->path().string() << std::endl;
        //当前的路径一定是一个合法的，以.html结束的普通网页文件
        files_list->push_back(iter->path().string()); //将所有带路径的html保存在files_list,方便后续进行文本分析
    }

    return true;
}

static bool ParseTitle(const std::string &file, std::string *title)
{
    std::size_t begin = file.find("<title>");
    if(begin == std::string::npos){
        return false;
    }
    std::size_t end = file.find("</title>");
    if(end == std::string::npos){
        return false;
    }

    begin += std::string("<title>").size();

    if(begin > end){
        return false;
    }
    *title = file.substr(begin, end - begin);
    return true;
}

static bool ParseContent(const std::string &file, std::string *content)
{
    //去标签,基于一个简易的状态机
    enum status{
        LABLE,
        CONTENT
    };

    enum status s = LABLE;
    for( char c : file){
        switch(s){
            case LABLE:
                if(c == '>') s = CONTENT;
                break;
            case CONTENT:
                if(c == '<') s = LABLE;
                else {
                    //我们不想保留原始文件中的\n,因为我们想用\n作为html解析之后文本的分隔符
                    if(c == '\n') c = ' ';
                    content->push_back(c);
                }
                break;
            default:
                break;
        }
    }

    return true;
}

static bool ParseUrl(const std::string &file_path, std::string *url)
{
    std::string url_head = "https://www.boost.org/doc/libs/1_78_0/doc/html";
    std::string url_tail = file_path.substr(src_path.size());

    *url = url_head + url_tail;
    return true;
}

//for debug
static void ShowDoc( const DocInfo_t &doc)
{
    std::cout << "title: " << doc.title << std::endl;
    std::cout << "content: " << doc.content << std::endl;
    std::cout << "url: " << doc.url << std::endl;
}

bool ParseHtml(const std::vector<std::string> &files_list, std::vector<DocInfo_t> *results)
{
    for(const std::string &file : files_list){
        //1. 读取文件，Read();
        std::string result;
        if(!ns_util::FileUtil::ReadFile(file, &result)){
            continue;
        }
        DocInfo_t doc;
        //2. 解析指定的文件，提取title
        if(!ParseTitle(result, &doc.title)){
            continue;
        }
        //3. 解析指定的文件，提取content,就是去标签
        if(!ParseContent(result, &doc.content)){
            continue;
        }
        //4. 解析指定的文件路径，构建url
        if(!ParseUrl(file, &doc.url)){
            continue;
        }

       
        results->push_back(std::move(doc)); 
        //ShowDoc(doc);

    }
    return true;
}

bool SaveHtml(const std::vector<DocInfo_t> &results, const std::string &output)
{
#define SEP '\3'
    //按照二进制方式进行写入
    std::ofstream out(output, std::ios::out | std::ios::binary);
    if(!out.is_open()){
        std::cerr << "open " << output << " failed!" << std::endl;
        return false;
    }

    //就可以进行文件内容的写入了
    for(auto &item : results){
        std::string out_string;
        out_string = item.title;
        out_string += SEP;
        out_string += item.content;
        out_string += SEP;
        out_string += item.url;
        out_string += '\n';

        out.write(out_string.c_str(), out_string.size());
    }

    out.close();

    return true;
}

```
将官网上下载的html文件都删去<>标签，然后以'\3'作为分隔符，将title、content、url写入文件，方便后续的文本分析。

# 建立索引文件

## 正排倒排的结构

```cpp
#pragma once

#include <iostream>
#include <string>
#include <vector>
#include <fstream>
#include <unordered_map>
#include <mutex>
#include "util.hpp"
#include "log.hpp"

namespace ns_index{

    struct DocInfo{
        std::string title;   //文档的标题
        std::string content; //文档对应的去标签之后的内容
        std::string url;     //官网文档url
        uint64_t doc_id;          //文档的ID
    };

    struct InvertedElem{
        uint64_t doc_id;
        std::string word;
        int weight;
        InvertedElem():weight(0){}
    };

    //倒排拉链
    typedef std::vector<InvertedElem> InvertedList;

    class Index{
        private:
            //正排索引的数据结构用数组，数组的下标天然是文档的ID
            std::vector<DocInfo> forward_index; //正排索引
            //倒排索引一定是一个关键字和一组(个)InvertedElem对应[关键字和倒排拉链的映射关系]
            std::unordered_map<std::string, InvertedList> inverted_index;
        private:
            Index(){} 
            Index(const Index&) = delete;
            Index& operator=(const Index&) = delete;

            static Index* instance;
            static std::mutex mtx;
        public:
            ~Index(){}
        public:
            static Index* GetInstance()
            {
                if(nullptr == instance){
                    mtx.lock();
                    if(nullptr == instance){
                        instance = new Index();
                    }
                    mtx.unlock();
                }
                return instance;
            }
            //根据doc_id找到找到文档内容
            DocInfo *GetForwardIndex(uint64_t doc_id)
            {
                if(doc_id >= forward_index.size()){
                    std::cerr << "doc_id out range, error!" << std::endl;
                    return nullptr;
                }
                return &forward_index[doc_id];
            }

            //根据关键字string，获得倒排拉链
            InvertedList *GetInvertedList(const std::string &word)
            {
                auto iter = inverted_index.find(word);
                if(iter == inverted_index.end()){
                    std::cerr << word << " have no InvertedList" << std::endl;
                    return nullptr;
                }
                return &(iter->second);
            }
            //根据去标签，格式化之后的文档，构建正排和倒排索引
            //data/raw_html/raw.txt
            bool BuildIndex(const std::string &input) //parse处理完毕的数据交给我
            {
                std::ifstream in(input, std::ios::in | std::ios::binary);
                if(!in.is_open()){
                    std::cerr << "sorry, " << input << " open error" << std::endl;
                    return false;
                }

                std::string line;
                int count = 0;
                while(std::getline(in, line)){
                    DocInfo * doc = BuildForwardIndex(line);
                    if(nullptr == doc){
                        std::cerr << "build " << line << " error" << std::endl; //for deubg
                        continue;
                    }

                    BuildInvertedIndex(*doc);
                    count++;

                    LOG(NORMAL, "当前的已经建立的索引文档: " + std::to_string(count));
                    
                }
                return true;
            }
        private:
            DocInfo *BuildForwardIndex(const std::string &line)
            {
                //1. 解析line，字符串切分
                //line -> 3 string, title, content, url
                std::vector<std::string> results;
                const std::string sep = "\3";   //行内分隔符
                ns_util::StringUtil::Split(line, &results, sep);
               
                if(results.size() != 3){
                    return nullptr;
                }
                //2. 字符串进行填充到DocIinfo
                DocInfo doc;
                doc.title = results[0]; //title
                doc.content = results[1]; //content
                doc.url = results[2];   ///url
                doc.doc_id = forward_index.size(); //先进行保存id，在插入，对应的id就是当前doc在vector中的下标!
                //3. 插入到正排索引的vector
                forward_index.push_back(std::move(doc)); //doc,html文件内容
                return &forward_index.back();
            }

            bool BuildInvertedIndex(const DocInfo &doc)
            {
                //DocInfo{title, content, url, doc_id}
                //word -> 倒排拉链
                struct word_cnt{
                    int title_cnt;
                    int content_cnt;

                    word_cnt():title_cnt(0), content_cnt(0){}
                };
                std::unordered_map<std::string, word_cnt> word_map; //用来暂存词频的映射表

                //对标题进行分词
                std::vector<std::string> title_words;
                ns_util::JiebaUtil::CutString(doc.title, &title_words);

                //对标题进行词频统计
                for(std::string s : title_words){
                    boost::to_lower(s); //需要统一转化成为小写
                    word_map[s].title_cnt++; //如果存在就获取，如果不存在就新建
                }

                //对文档内容进行分词
                std::vector<std::string> content_words;
                ns_util::JiebaUtil::CutString(doc.content, &content_words);

                //对内容进行词频统计
                for(std::string s : content_words){
                    boost::to_lower(s);
                    word_map[s].content_cnt++;
                }

#define X 10
#define Y 1
                //Hello,hello,HELLO
                for(auto &word_pair : word_map){
                    InvertedElem item;
                    item.doc_id = doc.doc_id;
                    item.word = word_pair.first;
                    item.weight = X*word_pair.second.title_cnt + Y*word_pair.second.content_cnt; //相关性
                    InvertedList &inverted_list = inverted_index[word_pair.first];
                    inverted_list.push_back(std::move(item));
                }

                return true;
            }
    };
    Index* Index::instance = nullptr;
    std::mutex Index::mtx;
}

```

处理过程我们拿到的文档内容是
struct DocInfo{
    std::string title;
    std::string content;
    std::string url;
    int doc_id;
};
我们需要识别为
title:
content:
url:
doc_id:

根据文档内容，形成一个或者多个倒排拉链
一个文档会有多个“词”,都会对应到当前的doc_id

我们需要对这些内容进行分词，使用jieba分词

i like to eat apple
分为i /like to /eat/ apple/eat apple；

然后需要对词和文档的相关性进行处理，（简化处理，只是用词频）
对title_word和content_word进行词频统计，赋予不同的权重

struct word_cnt{
    int title_cnt;
    int content_cnt;
};

```cpp
            //对内容进行词频统计
                for(std::string s : content_words){
                    boost::to_lower(s);
                    word_map[s].content_cnt++;
                }

#define X 10
#define Y 1
                //Hello,hello,HELLO
                for(auto &word_pair : word_map){
                    InvertedElem item;
                    item.doc_id = doc.doc_id;
                    item.word = word_pair.first;
                    item.weight = X*word_pair.second.title_cnt + Y*word_pair.second.content_cnt; //相关性
                    InvertedList &inverted_list = inverted_index[word_pair.first];
                    inverted_list.push_back(std::move(item));
                }
```
这里的权值设置的是标题为10，内容为1，可以根据实际需求进行调整。

# 编写搜索引擎模块

下面是搜索引擎的框架
我们首先要获得之前建立的索引对象
然后根据用户输入的query进行分词，根据分词结果，
在索引中查找对应的文档，
然后根据文档的相关性进行排序，最后将结果构建成json串返回给用户


```cpp
namespace ns_searcher {
class Searcher {
private:
    ns_index::Index* index; // 供系统进行查找的索引
public:
    Searcher() {}
    ~Searcher() {}

public:
    void InitSearcher(const std::string& input) {
        // 1. 获取或者创建index对象
        // 2. 根据index对象建立索引
    }
    // query: 搜索关键字
    // json_string: 返回给用户浏览器的搜索结果
    void Search(const std::string& query, std::string* json_string) {
        // 1.[分词]:对我们的query进行按照searcher的要求进行分词
        // 2.[触发]:就是根据分词的各个"词"，进行index查找
        // 3.[合并排序]：汇总查找结果，按照相关性(weight)降序排序
        // 4.[构建]:根据查找出来的结果，构建json串 -- jsoncpp
    }
  };
} 
```

回顾常规的浏览器搜索返回的三大件应该是：标题、摘要、url
需要对文档进行摘要处理，
首先获取文档的的内容，定义start,end，分别标定文档的前后界限
在内容中找到query中的词，然后根据词的位置，该词向前50，向后100（在不超过界限的前提下）形成摘要

# 编写http_server模块
需要使用cpp-httplib库


```cpp
#include "httplib.h"
#include "searcher.hpp"

const std::string input = "data/raw_html/raw.txt";
const std::string root_path = "./wwwroot";

int main()
{
    ns_searcher::Searcher search;
    search.InitSearcher(input);

    httplib::Server svr;

    svr.set_base_dir(root_path.c_str());
    svr.Get("/s", [&search](const httplib::Request &req, httplib::Response &rsp){
            if(!req.has_param("word")){
                rsp.set_content("必须要有搜索关键字!", "text/plain; charset=utf-8");
                return;
            }
            std::string word = req.get_param_value("word");
          
            LOG(NORMAL, "用户搜索的: " + word);
            std::string json_string;
            search.Search(word, &json_string);
            rsp.set_content(json_string, "application/json; charset=utf-8");
           
            });


    LOG(NORMAL, "服务器启动成功...");

    svr.listen("0.0.0.0", 8081);
    return 0;
}

```