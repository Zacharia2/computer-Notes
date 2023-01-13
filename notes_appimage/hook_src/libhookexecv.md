```c
#include <stdio.h>
#include <string.h>
#include <dlfcn.h>
#include <stdlib.h>

/* Author: https://github.com/Hackerl/
 * https://github.com/Hackerl/Wine_Appimage/issues/11#issuecomment-447834456
 * sudo apt-get -y install gcc-multilib
 * gcc -shared -fPIC -ldl libhookexecv.c -o libhookexecv.so
 * for i386: gcc -shared -fPIC -m32 -ldl libhookexecv.c -o libhookexecv.so
 * 
 * hook wine execv syscall. use special ld.so
 * 就干了一件事，就是加载ld.so 与 调用wine-preloader_hook
 * */

// C语言strlen 函数用来求字符串的长度（包含多少个字符）

typedef int(*EXECV)(const char*, char**);

// str 结束于。返回，str长度大于end,并且不相等的逻辑值
static inline int strendswith( const char* str, const char* end )
{
    size_t len = strlen( str );
    size_t tail = strlen( end );

    // && 如果两个操作数都非零，则条件为真。
    // ! 用来逆转操作数的逻辑状态。如果条件为真则逻辑非运算符将使其为假。
    // strcmp函数,用于比较两个字符串,结果用数字表示。相等为0（假），不等为真）
    // C语言中“0”为假，“1”为真。
    return len >= tail && !strcmp( str + len - tail, end );
}

// int execv(char *path, char ** argv)
// exec函数族的6个函数原型其中一个。
// exec是函数族提供了一个在进程中执行另一个进程的方法。
// 它可以根据指定的文件名或目录名找到可执行文件，并用它来取代原调用进程的数据段、
// 代码段和堆栈段，在执行完之后，原调用进程的内容除了进程号外，
// 其他全部被新程序的内容替换了。另外，这里的可执行文件既可以是二进制文件，
// 也可以是Linux下任何可执行脚本文件。

// char *path = "$HERE/lib/ld-linux.so.2"
// char ** argv  = "$HERE/opt/wine-stable/bin/wine" "$@"
int execv(char *path, char ** argv)
{
    static void *handle = NULL;
    static EXECV old_execv = NULL;
    char **last_arg = argv;

    if( !handle )
    {
        handle = dlopen("libc.so.6", RTLD_LAZY);
        old_execv = (EXECV)dlsym(handle, "execv");
    }

    // 加载WINELDLIBRARY环境变量
    char * wineloader = getenv("WINELDLIBRARY");

    if (wineloader == NULL)
    {
        return old_execv(path, argv);
    }

    // 分配内存
    while (*last_arg) last_arg++;

    // “C语言中malloc是动态内存分配函数。
    // “memcpy函数 c和c++使用的内存拷贝函数
    char ** new_argv = (char **) malloc( (last_arg - argv + 2) * sizeof(*argv) );
    memcpy( new_argv + 1, argv, (last_arg - argv + 1) * sizeof(*argv) );

    char * pathname = NULL;

    // memset 函数的功能是：将指针变量 hookpath 所指向的前 256 字节的内存单元用一个“整数” 0 替换，注意 c 是 int 型。
    // 就是初始化一个256字节的内存呗。
    // memset() 的作用是在一段内存块中填充某个给定的值。因为它只能填充一个值
    char hookpath[256];
    memset(hookpath, 0, 256);

    // 拼接wine-preloader_hook路径。
    // 判断path字符串长度大于"wine-preloader"并且两个参数不相等则拼接字符串。
    if (strendswith(path, "wine-preloader"))
    {
        // strcat(str,ptr)是将字符串ptr内容连接到字符串str后，然后得到一个组合后的字符串str
        strcat(hookpath, path);
        strcat(hookpath, "_hook");
        
        wineloader = hookpath; 
        // 现在可以调用wine-preloader_hook了。
    }

    new_argv[0] = wineloader;
    // 调用ine-preloader_hook(int argc, char ** argv)
    int res = old_execv(wineloader, new_argv);
    free( new_argv );

    // 返回替换好的execv（）
    return res;
}
```