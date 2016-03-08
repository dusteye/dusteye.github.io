---
layout: post
tags : [C++, C++11, folly]
category :
- C-Cpp
---

folly是facebook开源的一个C++底层库，采用c++11标准，主要用于提高大规模，高并发的应用性能。

###编译folly

根据folly的文档，目前folly只在ubuntu 12.04 64 bit的和Fedora 17 64bit上测试通过。在ubuntu 12.04 64 bit上编译folly遇到了诸多问题，以下是解决备忘：

* -依赖，folly依赖libboost, libboost-system, 可以安装libboost-all-dev包，只安装libboost-dev会在autoconf时候出错。
* -folly编译使用automake和autoconf工具，由于autoconf的不成熟，使用autoconf中会出现问题，使用autoreconf替代
* -依然是automake和autoconf的问题，github上有个[open issue](https://github.com/facebook/folly/pull/22)可以解决这个问题
* -一个头文件问题
Portability.h
<pre>
<code class="cpp">
    #ifdef __GNUC__
    # if __GNUC_PREREQ(4,7)
    #  define FOLLY_FINAL final
    #  define FOLLY_OVERRIDE override
    # endif
    #endif
</code>
</pre>
其中`__GNUC_PREREQ(4,7)`为features.h中的宏，需要include features.h

后续：以上问题部分最新版已解决
