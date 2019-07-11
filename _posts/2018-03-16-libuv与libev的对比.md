---
layout: article
title: libuv 与 libev 的对比
key: 20180316
tags: c/c++ libuv libev
---

# libuv 与 libev 的对比

[转载加工自 http://blog.csdn.net/nanjunxiao/article/details/9066077](http://blog.csdn.net/nanjunxiao/article/details/9066077)
## 异步 VS 同步
- libuv是异步的，libev是同步的多路IO复用。
- libev 是系统IO复用的简单封装，基本上来说，它解决了 epoll ，kqueuq 与 select 之间 API 不同的问题。保证使用 livev 的 API 编写出的程序可以在大多数 *nix 平台上运行。但是libev 的缺点也是显而易见，由于基本只是封装了 Event Library，用起来有诸多不便。比如accept(3) 连接以后需要手动 setnonblocking 。从 socket 读写时需要检测 EAGAIN、EWOULDBLOCK 和 EINTER 。这也是大多数人认为异步程序难写的根本原因。
- libuv 则显得更为高层。libuv 是 joyent 给 Node 做的一套 I/O Library 。而这也导致了 libuv 最大的特点就是处处回调。基本上只要有可能阻塞的地方，libuv 都使用回调处理。这样做实际上大大减轻了程序员的工作量。因为当回调被 call 的时候，libuv 保证你有事可做，这样 EAGAIN和 EWOULDBLOCK 之类的 handle 就不是程序员的工作了，libuv 会默默的帮你搞定。
## 读写事件处理方式
- libev 在 socket 发生读写事件时，只告诉你，“XX socket 可以读/写了，自己看着办吧”。往往我们需要自己申请内存并调用 read(3) 或者 write(3) 来响应 I/O 事件。

- libuv 则稍微复杂一些，我们分读/写两个部分来描述。

   > 当接口可读时，libuv 会调用你的 allocate callback 来申请内存并将读到的内容写入。当读取完毕后，libuv 会 call 你为这个 socket 设置的回调函数，在参数中带着这个 buffer 的信息。你只需要负责处理这个 buffer 并且 free 掉就OK了。因为是从 buffer 中读取数据，在你的 callback 被调用时数据已经 ready 了，所以程序员也就不用考虑阻塞的问题了。

    > 而对写的处理则更显巧妙。libuv 没有 write callback ，如果你想写东西，直接 generate 一个 write request 连着要写的 buffer 一起丢给 libuv ，libuv 会把你的 write request 加进相应 socket 的 write queue ，在 I/O 可写时按顺序写入。
    >
## 读写上下文处理
- C 没有闭包，所以确定读写上下文是 libuv 的使用者需要面对的问题。否则程序面对汹涌而来的 buffer 也不能分得清哪个是哪个的数据。在这一点的处理上，libuv 跟 libev 一样，都是使用了一个 void *data 来解决问题。你可以用 data 这个 member 存储任何东西，这样当 buffer 来的时候，只需要简单的把 data cast 到你需要的类型就 OK 了。

## 异步 DNS 解析
- libev 没有异步 DNS 解析，这一点一直广为垢病。

- libuv 有异步的 DNS 解析，解析结果也是通过回调的方式通知程序。

## 单线程 VS 多线程
- libev 完全是单线程的。

- libuv 需要多线程库支持，因为其在内部维护了一个线程池来 handle 诸如 getaddrinfo(3) 这样的无法异步的调用。

## 开发支持
- libev 貌似是作者一个人在开发，版本管理使用的还是 CVS ，社区参与度明显不高。

- libuv 社区十分活跃，几乎每天都有人提出 Issue 并贡献代码。

## WINDOWS IOCP支持
- libev 不支持 IOCP ，如果需要在 Win 下运行的程序会很麻烦。

- libuv 支持 IOCP ，有相应脚本编译 Win 下的库。

## Q&A
Q: 博主有没做过两者的benchmark，他们之前的性能对比如何？

A: 当时用 libev 和 libuv 写过一个简单的 HTTP Hello World Server 。具体结果记不清楚了但是可以说性能差距在 5% 以内。

Q:  libuv 在 unix 上应该是用 libev 作为 non-blocking IO 的实现的吧？libuv 中线程池里线程的数量会增加么，是否会有上限？如果上限到了是不是就会出现 block 的情况？

A: 1. libuv 在大概5个月前已经完全不使用 libev 了，参见 commit665a316aa9d551ffdd00d1192d0c3d9c88d7e866 ; 2. libuv 的线程池在BSS上，数量固定为4个，参见：https://github.com/joyent/libuv/blob/master/src/unix/threadpool.c#L28 ; 3. libuv 的线程池共享一个work queue ，所以不会出现 block 的情况



libevent : 名气最大，应用最广泛，历史悠久的跨平台事件库；
libev : 较libevent而言，设计更简练，性能更好，但对Windows支持不够好；
libuv : 开发node的过程中需要一个跨平台的事件库，他们首选了libev，但又要支持Windows，故重新封装了一套，*nix下用libev实现，Windows下用IOCP实现；

## 参考
- [库-libuv 和 libev的对比](http://www.blog.chinaunix.net/uid-28458801-id-4463981.html)
