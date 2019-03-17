---
title: C++基础
tags:
---



### 安装g++编译器 

```bash
sudo apt-get install build-essential
gcc --version
```



### 编译源文件

```C++
//《hello.cpp》源文件内容：

#include <iostream>
using namespace std;
int main() {
   cout << "Hello, world!!!!" << endl;
   return 0;
}

// 编译hello.cpp   （-c 表示只编译，不链接）
g++ -c hello.cpp

// 链接hello.o生成hello.out (-o 表示输出文件)
g++ -o hello.out hello.cpp

// 运行hello.out
./hello.out
```

### 构建项目

```C++
// .h和.cpp文件相互配合 需要用	Make工具来构建项目

# hw2.cpp
#include "solution.h"
int main () {
    Solution sln;
    sln.Say();
    return 0;
}

# solution.h
/* solution.h */
class Solution {
public:
   void Say();
};

# solution.cpp
/* solution.cpp */
#include <iostream>
#include "solution.h"
void Solution::Say(){
   std::cout << "HI!!!!!!" << std::endl;
}

// 创建一个makefile文件，以告诉Make如何编译和链接程序
# 生成可执行文件build，prerequisites有两个.o文件，是因为代码里hw2引用了solution.h。
build : hw2.o solution.o
    g++ -o build hw2.o solution.o #注意前面必须是tab，不能是空格
# 编译hw2.cpp，生成hw2.o文件，-g 表示生成的文件可用gdb调试，如果没有-g，调试时无法命中断点
hw2.o : hw2.cpp solution.h
    g++ -g -c hw2.cpp
# 编译solution.cpp文件，生成solution.o文件。
solution.o : solution.h solution.cpp
    g++ -g -c solution.cpp
# 清除标签: make不找冒号后的依赖关系，也不自动执行命令。如果要执行该命令，必须在make后指出动作名字，如make clean
clean :
    rm hw2.o solution.o build
    
# makefile的格式:
target ... : prerequisites ...(空格区分多个文件)
　　command    #注意前面是tab    
// target这一个或多个目标，依赖于prerequisites列表中的文件，其执行规则定义在command里。
// 如果prerequisites列表中文件比target要新，就会执行command，否则就跳过。

// make命令的流程
1 make在当前目录下找名为makefile或Makefile的文件；
2 如果找到，它会找文件中的第一个target，如上述文件中的build，并作为终极目标文件;
3 如果第一个target的文件不存在，或其依赖的.o 文件修改时间要比target这个文件新，则会执行紧接着的command来生成这个target文件;
4 如果第一个target所依赖的.o文件不存在，则会在makefile文件中找target为.o的依赖，如果找到则执行command，.o的依赖必是.h或.cpp，于是make可以生成 .o 文件了
5 回溯到第2步执行最终目标

./build # 执行文件


// makefile:2: *** missing separator。 停止。  可能是Tab被替换成了空格~
```



#### VSCode 配置 makefile用tab(不替换成空格)

"[makefile]": {

        "editor.quickSuggestions": false,
    
        "editor.formatOnSave": true,
    
        "editor.renderWhitespace": "all",
    
        "editor.acceptSuggestionOnEnter": "off",
    
        "editor.detectIndentation": false,
    
    }