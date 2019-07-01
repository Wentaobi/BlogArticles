## [boost_regex 1.55.0](https://www.boost.org/doc/libs/1_55_0/libs/regex/doc/html/boost_regex/ref/basic_regex.html)
## [boost - 正则表达式xpressive](https://www.cnblogs.com/MakeView660/p/7099474.html)
## [C++遍历文件夹，使用boost filesystem递归遍历文件夹](https://www.cnblogs.com/sharpstill/archive/2012/02/21/2361057.html)
```cpp
#ifndef SCANALLFILES_H
#define SCANALLFILES_H
#include "boost/filesystem/operations.hpp"
#include "boost/filesystem/path.hpp"
#include <iostream>
using namespace std;

class ScanAllFiles{
public:
    static const vector<string>& scanFiles(const string&,vector<string>&); //方法一,自己写递归，用filesystem里的directory_iterator
    static const vector<string>& scanFilesUseRecursive(const string&,vector<string>&); //方法二，直接用boost的filesystem里的recursive_directory_iterator
};
//方法一，自己写递归
const vector<string>& ScanAllFiles::scanFiles(const string& rootPath,vector<string>& container=*(new vector<string>())){
    namespace fs = boost::filesystem;
    fs::path fullpath (rootPath, fs::native);
    vector<string> &ret = container;
   
    if(!fs::exists(fullpath)){return ret;}
    fs::directory_iterator end_iter;  /**无参构造函数是最后那个iterator的value 摘抄如下
*If the end of the directory elements is reached, the iterator becomes equal to the end iterator value. The constructor directory_iterator() with no arguments always constructs an end iterator object, which is the only legitimate iterator to be used for the end condition. The result of operator* on an end iterator is not defined. For any other iterator value a const directory_entry& is returned. The result ofoperator-> on an end iterator is not defined. For any other iterator value a const directory_entry* is returned.
*
**/
    for(fs::directory_iterator iter(fullpath);iter!=end_iter;iter++){
        try{
            if (fs::is_directory( *iter ) ){
                std::cout<<*iter << "is dir.whose parent path is " << iter->path().branch_path() << std::endl;
                ret.push_back(iter->path().string()); //递归前push_back进去一个
                ScanAllFiles::scanFiles(iter->path().string(),ret);//递归，把vector也传进去
            }else{
                ret.push_back(iter->path().string());
                std::cout << *iter << " is a file" << std::endl;
            }
        } catch ( const std::exception & ex ){
            std::cerr << ex.what() << std::endl;
            continue;
        }
    }
    return ret;
}
//方法二，直接用boost的filesystem里的recursive_directory_iterator
const vector<string>& ScanAllFiles::scanFilesUseRecursive(const string& rootPath,vector<string>& container=*(new vector<string>())){
    namespace fs = boost::filesystem;
    fs::path fullpath (rootPath, fs::native);
    vector<string> &ret = container;
   
    if(!fs::exists(fullpath)){return ret;}
    fs::recursive_directory_iterator end_iter;
    for(fs::recursive_directory_iterator iter(fullpath);iter!=end_iter;iter++){
        try{
            if (fs::is_directory( *iter ) ){
                std::cout<<*iter << "is dir" << std::endl;
                ret.push_back(iter->path().string());
                //ScanAllFiles::scanFiles(iter->path().string(),ret);
            }else{
                ret.push_back(iter->path().string());
                std::cout << *iter << " is a file" << std::endl;
            }
        } catch ( const std::exception & ex ){
            std::cerr << ex.what() << std::endl;
            continue;
        }
    }
    return ret;
}
#endif
```
另外，转载一篇ibm的boost filesystem入门文章:http://www.ibm.com/developerworks/cn/aix/library/au-boostfs/
还有一个boost的filesystem的conference: http://www.boost.org/doc/libs/1_48_0/libs/filesystem/v3/doc/reference.html#Class-directory_entry
