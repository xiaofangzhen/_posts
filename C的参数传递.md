title: C的参数传递
date: 2020-02-11 16:40:12
mathjax: true
tags: C
---

1.先来看一个经典的笔试题


``` bash
void func(char *p) {
    p = (char *)malloc(100);
}
```

``` bash
int main ( int argc, char *argv[] )  {
    char *p;
    func(p);
    char s[] = "hello world";
    strcpy(p,s);
    printf("%s\n",p);
    return EXIT_SUCCESS;
}
```

编译运行后，不出意外会出现段错误，为什么呢？
这里需要理解清楚指针作为参数进行的值传递
指针在C里也是一个变量，有分配内存，内存里存的是指针指向的地址。所以指针作为参数进行传递的时候，实际上传递的是指针这个值。
先来看个例子：


``` bash
void func(char *p) {
    printf("%lld %lld\n",&p,p);
}
```

``` bash
int main ( int argc, char *argv[] )  {
    char *p = "1";
    printf("%lld %lld\n",&p,p);
    func(p);
    return EXIT_SUCCESS;
}
```

运行后可以看到两个&p是不同的，两个p是一样的。也就是在调用func时，系统新建了一个临时指针，这两个临时指针指向同个地方。
现在就很好理解为什么前面的程序会段错误。

``` bash
void func(char *p) {
    p = (char *)malloc(100);
}
```

因为，在这个函数里，只是将系统新建的临时指针指向了新分配的内存。而作为值传递，main中的p指向的地址并没有被改变。

也就很好理解为什么传递指针的时候可以改变指针的内容。因为虽然是两个指针，但指向了同个地址
``` bash
void func ( int * p ){
     *p = 2；
}
```
``` bash
int main ( int argc, char *argv[] )
{
    int a = 1;
    int *p = &a;
    func(p);
    printf("%d\n",*p);
    return EXIT_SUCCESS;
}
```
打印：2


注意：在C语言中都是传值的，传引用是C++的特性
