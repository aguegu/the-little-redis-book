# About This Book
# 关于本书

## License
## 许可证

The Little Redis Book is licensed under the Attribution-NonCommercial 3.0 Unported license. You should not have paid for this book.

《Redis小册子》使用《署名-非商业性使用 3.0 未本地化版本》的CC开源协议。您不应为此书付出费用。

You are free to copy, distribute, modify or display the book. However, I ask that you always attribute the book to me, Karl Seguin, and do not use it for commercial purposes.

您可以自由的复制、传播、修改以及展示本书。不过，我要求您永远保留本书的署名权是我的，Karl Seguin，并不将此书用作商业用途。

You can see the *full text* of **the license at**:
您可以在这里查看到该**协议**的*全部内容*：

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

## About The Author
## 关于作者

Karl Seguin is a developer with experience across various fields and technologies. He's an active contributor to Open-Source Software projects, a technical writer and an occasional speaker. He's written various articles, as well as a few tools, about Redis. Redis powers the ranking and statistics of his free service for casual game developers: [mogade.com](http://mogade.com/).

Karl Seguin 是在多个领域以及技术方面都有经验的开发者。他是开源软件项目的积极贡献者，技术作家还时不时进行演讲。关于Redis，他已经写了多篇论文，以及一些工具。Redis帮助他在其不定期义务参与的游戏开发中提升等级以及统计数据。

Karl wrote [The Little MongoDB Book](http://openmymind.net/2011/3/28/The-Little-MongoDB-Book/), the free and popular book about MongoDB.

Karl 还写了一本免费而且相当流行的关于MongoDB的书：[MongoDB小册子](http://openmymind.net/2011/3/28/The-Little-MongoDB-Book/)。

His blog can be found at <http://openmymind.net> and he tweets via [@karlseguin](http://twitter.com/karlseguin)

作者的博客：<http://openmymind.net>，twitter：[@karlseguin](http://twitter.com/karlseguin)

## With Thanks To
## 致谢

A special thanks to [Perry Neal](https://twitter.com/perryneal) for lending me his eyes, mind and passion. You provided me with invaluable help. Thank you.
特别感谢[Perry Neal](https://twitter.com/perryneal)，用他的注意力、思考和激情来帮助我，他的帮助无比珍贵，在此表达感谢。

## Latest Version
## 最新版本

The latest source of this book is available at:
<http://github.com/karlseguin/the-little-redis-book>

可以在<http://github.com/karlseguin/the-little-redis-book>这里找到本书的最新版本。

# Introduction
# 简介

Over the last couple years, the techniques and tools used for persisting and querying data have grown at an incredible pace. While it's safe to say that relational databases aren't going anywhere, we can also say that the ecosystem around data is never going to be the same.

最近二十年来，用来存储和查询数据的技术和工具发展相当迅猛。虽然我们依然能说关系数据库估计不会再有什么大动静，但我们能说现在数据的生态已经完全今非夕比了。

Of all the new tools and solutions, for me, Redis has been the most exciting. Why? First because it's unbelievably easy to learn. Hours is the right unit to use when talking about length of time it takes to get comfortable with Redis. Secondly, it solves a specific set of problems while at the same time being quite generic. What exactly does that mean? Redis doesn't try to be all things to all data. As you get to know Redis, it'll become increasingly evident what does and what does not belong in it. And when it does, as a developer, it's a great experience.

在所有的新工具和解决方案中，对于我来说，Redis是最让人兴奋的。究其缘由，首先，学习它超级简单，要掌握Redis说需要的时间，是以小时为单位的。第二，它解决一个普遍存在的许多问题。这是什么意思呢？Redis并未试图成为所有数据的万能药。随着您对Redis的不断了解，您会越来越qinxi清晰地了解到Redis能做什么，不能做什么。当了解了这些概念之后，作为开发者来说，这将是非常有益的经验。

While you can build a complete system using Redis only, I think most people will find that it supplements their more generic data solution - whether that be a traditional relational database, a document-oriented system, or something else. It's the kind of solution you use to implement specific features. In that way, it's similar to an indexing engine. You wouldn't build your entire application on Lucene. But when you need good search, it's a much better experience - for both you and your users. Of course, the similarities between Redis and indexing engines end there.

虽然您可以玩完全用Redis构建一个完整的系统，但我想对于大多数人来说，Redis是对通用数据解决方案的补充，无论是传统的关系数据库，还是面向文本的系统，还是其它类型。Redis是用来弥补某些特殊功能的。从这个角度来理解，Redis更类似与是一个索引引擎。你不会把你的整个应用都用Lucene实现。但如果你需要强大的搜索，Lucence未您以及您的用户提供好得多的体验，当然，Redis和索引引擎的相似指出也就到此为止了。

The goal of this book is to build the foundation you'll need to master Redis. We'll focus on learning Redis' five data structures and look at various data modeling approaches. We'll also touch on some key administrative details and debugging techniques.

本书的目的在于为您掌握Redis打好基础。我们将重点学习Redis的物种数据结构，并研究多种数据建模的方法。我们还会接触到一些关键的管理细节以及调试技术。

# Getting Started
# 新手上路

We all learn differently: some like to get their hands dirty, some like to watch videos, and some like to read. Nothing will help you understand Redis more than actually experiencing it. Redis is easy to install and comes with a simple shell that'll give us everything we need. Let's take a couple minutes and get it up and running on our machine.

人们的学习方法各有不同：有些人喜欢动手实干，有些人喜欢观看视频，有些人则喜欢阅读。没有什么比真切地去感受Redis更能让你了解它。Redis安装非常简单，并自带简单的shell，这就提供了您所需要的一切。让我们花几分钟把Redis装上并运行起来。

## On Windows
## Windows平台

Redis itself doesn't officially support Windows, but there are options available. You wouldn't run these in production, but I've never experienced any limitations while doing development.

Redis官方并不支持windows，不过还是有招。你不应该在上线阶段使用windows上的redis。不过在自己开发的过程中，我还没遇到什么限制。

A port by Microsoft Open Technologies, Inc. can be found at <https://github.com/MSOpenTech/redis>. As of this writing the solution is not ready for use in production systems.

微软开发技术公司提供了一个移植版本：<https://github.com/MSOpenTech/redis>。在写著本书的时候，这个版本还没准备好投入到生产系统中。

Another solution, which has been available for some time, can be found at <https://github.com/dmajkic/redis/downloads>. You can download the most up to date version (which should be at the top of the list). Extract the zip file and, based on your architecture, open either the `64bit` or `32bit` folder.

另一个解决方案，也能用有段时间了：<https://github.com/dmajkic/redis/downloads>。您可以下载其最新的版本(一般在列表最顶部)，解压zip文件，基于您的系统的架构，选择“64bit”或“32bit”的文件夹。

## On *nix and MacOSX
## *nix 和 MaxOSX 平台

For *nix and Mac users, building it from source is your best option. The instructions, along with the latest version number, are available at <http://redis.io/download>. At the time of this writing the latest version is 2.6.2; to install this version we would execute:

对于＊nix和Mac的用户来说，直接从源码编译是最好的选择。教程以及最新的版本号，可在<http://redis.io/download>查得。在写著本书时，最新的版本为2.6.2；安装只需要按照如下步骤执行：

    wget http://redis.googlecode.com/files/redis-2.6.2.tar.gz
	tar xzf redis-2.6.2.tar.gz
	cd redis-2.6.2
	make

(Alternatively, Redis is available via various package managers. For example, MacOSX users with Homebrew installed can simply type `brew install redis`.)
（此外，Redis也能够通过多种软件包管理工具进行安装。例如，使用Homebrew的MacOSX用户，只需要输入`brew install redis`即可）。

If you built it from source, the binary outputs have been placed in the `src` directory. Navigate to the `src` directory by executing `cd src`.

如果您是从源码编译，生成的二进制文件将保存在src文件夹内。要进入`src`文件夹，只需要执行`cd src`即可。

## Running and Connecting to Redis
## 运行并连接到Redis

If everything worked, the Redis binaries should be available at your fingertips. Redis has a handful of executables. We'll focus on the Redis server and the Redis command line interface (a DOS-like client). Let's start the server. In Windows, double click `redis-server`. On *nix/MacOSX run `./redis-server`.

如果一切正常，Redis的可执行文件应该唾手可得。我们将着眼于Redis服务器以及它的命令行界面（类似与Dos的客户端）。让我们启动Redis服务器吧。在windows平台，双击`redis-server`；在*ni/MacOSX平台，执行`./redis-server`

If you read the start up message you'll see a warning that the `redis.conf` file couldn't be found. Redis will instead use built-in defaults, which is fine for what we'll be doing.

如果你读了启动消息，您将会看到一个警告`redis.conf`文件无法找到。Redis将会使用其内置的默认配置文件，这个对于我们接下来的操作没有什么影响。

Next start the Redis console by either double clicking `redis-cli` (Windows) or running `./redis-cli` (*nix/MacOSX). This will connect to the locally-running server on the default port (6379).

接下来，我们要一个Redis控制台程序，要么是双击`redis-cli`程序（Windows）或执行`./redis-cli` (*nix/MacOSX)。这个控制台就连接到本地运行的服务器，其默认端口号为6379。

You can test that everything is working by entering `info` into the command line interface. You'll hopefully see a bunch of key-value pairs which provide a great deal of insight into the server's status.

我们可以通过在命令行界面键入`info`命令测试服务器的属性。您一般是可以看到一组键-值对，提供了大量服务器状态的各种参数。

If you are having problems with the above setup I suggest you seek help in the [official Redis support group](https://groups.google.com/forum/#!forum/redis-db).

如果您在以上安装过程中遇到任何问题，建议您查看[官方的帮助文档](https://groups.google.com/forum/#!forum/redis-db)。

# Redis Drivers
# Redis 驱动

As you'll soon learn, Redis' API is best described as an explicit set of functions. It has a very simple and procedural feel to it. This means that whether you are using the command line tool, or a driver for your favorite language, things are very similar. Therefore, you shouldn't have any problems following along if you prefer to work from a programming language. If you want, head over to the [client page](http://redis.io/clients) and download the appropriate driver.

就像您即将学习到的，Redis的API的最佳表现形式就是详细的函数说明。它非常简单而且规范。这就意味着无论您是使用命令行界面，还是使用您所钟爱的语言驱动，它们的使用方法都非常接近。所以，即便您需要通过某种编程语言来了解Redis也不应该遇到任何问题。如果您想这么做的话，可以转向[客户端页面](http://redis.io/clients)来下载相应的语言驱动。

# Chapter 1 - The Basics
# 第1章 - 基础

What makes Redis special? What types of problems does it solve? What should developers watch out for when using it? Before we can answer any of these questions, we need to understand what Redis is.

是什么让Redis与众不同呢？它又解决了哪些问题呢？开发者在使用它的时候需要注意那些问题？在我们回答以上所有问题之前，我们首先要了解Redis是什么。

Redis is often described as an in-memory persistent key-value store. I don't think that's an accurate description. Redis does hold all the data in memory (more on this in a bit), and it does write that out to disk for persistence, but it's much more than a simple key-value store. It's important to step beyond this misconception otherwise your perspective of Redis and the problems it solves will be too narrow.

Redis常被描述为是一种基于内存持久化的Key-Value（键-值）数据库，我认为这种描述还有失准确。Redis确实将所有的数据都保存在内存中，而且通过将数据写入磁盘以持久保存，但它远非简单的Key-Value数据库。务必要跨过这个误区，否则您对于Redis的观念将变得想当狭隘，而难以将它推广应用到更广阔的领域。 

The reality is that Redis exposes five different data structures, only one of which is a typical key-value structure. Understanding these five data structures, how they work, what methods they expose and what you can model with them is the key to understanding Redis. First though, let's wrap our heads around what it means to expose data structures.

现实情况是Redis拥有5种数据结构，只有其中的一种是典型的key-value结构。掌握这五种数据结构，它们如何运作，各自具备什么样的方法， 能应用到什么样的数据模型，是掌握Redis的关键。首先，让我们揭开这5种数据结构的神秘面纱吧。

If we were to apply this data structure concept to the relational world, we could say that databases expose a single data structure - tables. Tables are both complex and flexible. There isn't much you can't model, store or manipulate with tables. However, their generic nature isn't without drawbacks. Specifically, not everything is as simple, or as fast, as it ought to be. What if, rather than having a one-size-fits-all structure, we used more specialized structures? There might be some things we can't do (or at least, can't do very well), but surely we'd gain in simplicity and speed?

如果我们用这种数据结构的概念来审视传统的关系数据库，我们可以说那些数据库只有一种数据结构——表。表既复杂又有延展性。不能用表来建模、存储、操作的数据屈指可数。然而，它们的通用属性并不是百利而无一害的。尤其是，并不是所有数据都能像它们原本应当地那样的简单而快速。比方说，不采用一个尺寸能适应所有数据的结构，而是更加序列化的结构？有些事情我们做不到了（至少做不好），但能否在简单性和速度方面能有所提升？

Using specific data structures for specific problems? Isn't that how we code? You don't use a hashtable for every piece of data, nor do you use a scalar variable. To me, that defines Redis' approach. If you are dealing with scalars, lists, hashes, or sets, why not store them as scalars, lists, hashes and sets? Why should checking for the existence of a value be any more complex than calling `exists(key)` or slower than O(1) (constant time lookup which won't slow down regardless of how many items there are)?

针对特定的问题采用特定的数据结构，这不正是我们编程的方法么？你不会将所有的数据都放在一个哈希表里，也不会每个都定义为一个string变量。对于我来说，这就定义了Redis的处事之道。如果你处理的数据本身就是string，lists，hash或是sets，那么为什么不直接将它们存储为string，lists，hash或是sets。我们只检验一个值是否存在的操作要比调用`exists(key)`更复杂，或比O(1)还慢（静态查询时间，不会因为数据集合的规模影响）？

# The Building Blocks
# 基本元素

## Databases
## 数据库

Redis has the same basic concept of a database that you are already familiar with. A database contains a set of data. The typical use-case for a database is to group all of an application's data together and to keep it separate from another application's.

Redis中数据库的基本概念与您已经熟知的相同。数据库包含一组数据。数据库的典型应用案例就是将某个应用的所有数据分组集合在一起，并与别的应用的数据分离开。

In Redis, databases are simply identified by a number with the default database being number `0`. If you want to change to a different database you can do so via the `select` command. In the command line interface, type `select 1`. Redis should reply with an `OK` message and your prompt should change to something like `redis 127.0.0.1:6379[1]>`. If you want to switch back to the default database, just enter `select 0` in the command line interface.

在Redis中，数据库只是由简单的一个数字来进行标识的，默认值为0。如果你想要切换到不同的数据库中，可以通过“select”命令。在命令行界面内，输入“select 1”。Reids就会回复一个“OK”提示，您的命令提示符就会变为“redis 127.0.0.1:6379[1]>”，如果需要切换回默认的数据库，只需要在命令行输入“select 0”即可。

## Commands, Keys and Values
## 命令，键和值

While Redis is more than just a key-value store, at its core, every one of Redis' five data structures has at least a key and a value. It's imperative that we understand keys and values before moving on to other available pieces of information.

Redis并不仅仅是一个"键-值"存储仓库，不过在它的核心，每个数据，无论它是其五种数据结构中的那一种，都至少拥有一个键和一个值。在我们继续学习之前，我们的首要任务是理解redis的键和值。

Keys are how you identify pieces of data. We'll be dealing with keys a lot, but for now, it's good enough to know that a key might look like `users:leto`. One could reasonably expect such a key to contain information about a user named `leto`. The colon doesn't have any special meaning, as far as Redis is concerned, but using a separator is a common approach people use to organize their keys.

键是对每条数据的定义，我们将大量围绕键展开操作。但现在，只需要了解一个键可能看起来像“users:leto”。大家大概可以合理地推断出这个键包含的数据是关于一个名为“leto”的用户。冒号“：”并没有特殊的意义，至少Redis并不关心，但使用这样的分隔符，是人们常用的用于组织管理键的常用方法。

Values represent the actual data associated with the key. They can be anything. Sometimes you'll store strings, sometimes integers, sometimes you'll store serialized objects (in JSON, XML or some other format). For the most part, Redis treats values as a byte array and doesn't care what they are. Note that different drivers handle serialization differently (some leave it up to you) so in this book we'll only talk about string, integer and JSON.

值代表与键关联的具体数据。它可以是任意类型，可以是字符串、整形数据，甚至是存储的序列化对象（以JSON、XML或其它形式）。在大多数情况，Redis只是将值当作字节数组，而并不关心其具体内容。值得逐一的是，不同的驱动会以不同的方式处理序列化数据（有些会由用户决定）。这里，我们只会介绍有关字符串、整形和JSON的情况。

Let's get our hands a little dirty. Enter the following command:

我们动手开始干吧，输入以下命令：

	set users:leto "{name: leto, planet: dune, likes: [spice]}"
    
This is the basic anatomy of a Redis command. First we have the actual command, in this case `set`. Next we have its parameters. The `set` command takes two parameters: the key we are setting and the value we are setting it to. Many, but not all, commands take a key (and when they do, it's often the first parameter). Can you guess how to retrieve this value? Hopefully you said (but don't worry if you weren't sure!):

这就是一条Redis命令的基本结构。首先我们输入实际命令，在本例中就是“set”。接下来我们输入它的参数。"set"命令需要两个参数：我们指定的键，以及它所对应的值。绝大多数命令都以键作为输入参数（这时候，键通常作为第一参数）。是不是能猜出如何获取键所对应的值？希望您能立马反应上来。（不缺定也不要紧哈！）

	get users:leto

Go ahead and play with some other combinations. Keys and values are fundamental concepts, and the `get` and `set` commands are the simplest way to play with them. Create more users, try different types of keys, try different values.

放手去尝试其它的组合吧。键和值是最基本的概念，“get”和“set”是操作它们最简单的命令。创建更多的用户，并尝试不同的键和值吧。

## Querying
## 查询

As we move forward, two things will become clear. As far as Redis is concerned, keys are everything and values are nothing. Or, put another way, Redis doesn't allow you to query an object's values. Given the above, we can't find the user(s) which live on planet `dune`.

随着我们学习深入，有两个概念会变得清晰起来。对Redis来说，键就是一切，而值毫无意义。或者换种说法，，Redis不允许你对对象的值进行查询。鉴于此，我们无法查询出所有居住在“dune”星球上的用户。

For many, this will cause some concern. We've lived in a world where data querying is so flexible and powerful that Redis' approach seems primitive and unpragmatic. Don't let it unsettle you too much. Remember, Redis isn't a one-size-fits-all solution. There'll be things that just don't belong in there (because of the querying limitations). Also, consider that in some cases you'll find new ways to model your data.

对于大多数人来说，这可能引起一些顾虑。我们所了解的数据库中数据查询是那么地灵活和强大，但Redis的招数看起来低级而且不敏捷。别让这种顾虑太过于困扰你。Redis并不是一个大小通吃的解决方案。同时，考虑一下在有些情况下我们可以使用新的方法来重新组织我们的数据。

We'll look at more concrete examples as we move on, but it's important that we understand this basic reality of Redis. It helps us understand why values can be anything - Redis never needs to read or understand them. Also, it helps us get our minds thinking about modeling in this new world.

接下来我们会看到更加具体的例子，但首先我们需要了解到Redis这一实际特性。这就有助于我们了解为什么值可以是任何东西。Redis从未需要读取或是理解它们。而且，这也有助于我们思考在这种新环境下对数据如何建模。

## Memory and Persistence
## 内存与持久化

We mentioned before that Redis is an in-memory persistent store. With respect to persistence, by default, Redis snapshots the database to disk based on how many keys have changed. You configure it so that if X number of keys change, then save the database every Y seconds. By default, Redis will save the database every 60 seconds if 1000 or more keys have changed all the way to 15 minutes if 9 or less keys has changed.

之前我们提到Redis是一种内存持久化存储。为了持久化的需要，在默认情况下，Redis依据多少键发生改变将数据快照保存到磁盘。你可以自定义设置，这样如果数量位X的键发生了改变，那么就将数据库每Y秒保存一次。在默认情况下，Redis可以快到在1000以上个键发生了变化的情况下，每60秒保存一次数据库；慢到当9个以下的键发生变化时15分钟一次。

Alternatively (or in addition to snapshotting), Redis can run in append mode. Any time a key changes, an append-only file is updated on disk. In some cases it's acceptable to lose 60 seconds worth of data, in exchange for performance, should there be some hardware or software failure. In some cases such a loss is not acceptable. Redis gives you the option. In chapter 6 we'll see a third option, which is offloading persistence to a slave.

另外，在系统快照的基础上，Redis还能运行为追加模式。每次键值变化，只在磁盘上保存一个追加记录。在有些情况下，比如为了获取性能表现，或在软硬件故障的情况下，丢失60秒的数据以是可以被允许的。但在另外一些情况下，这种损失是坚决不允许的。Redis将选择权交给您。在第6章，我们可以看到第三种选项，我们可以将载荷分担到从机上。

With respect to memory, Redis keeps all your data in memory. The obvious implication of this is the cost of running Redis: RAM is still the most expensive part of server hardware.

内存方面，Redis将所有数据都保存在内存中，这明显意味这就是运行redis的代价，内存依然是服务器硬件配置中最贵的部分。

I do feel that some developers have lost touch with how little space data can take. The Complete Works of William Shakespeare takes roughly 5.5MB of storage. As for scaling, other solutions tend to be IO- or CPU-bound. Which limitation (RAM or IO) will require you to scale out to more machines really depends on the type of data and how you are storing and querying it. Unless you're storing large multimedia files in Redis, the in-memory aspect is probably a non-issue. For apps where it is an issue you'll likely be trading being IO-bound for being memory bound.

我真切地感受到有些开发者已经忘记了数据所占用的空间是多么地小。就拿莎士比亚全集来说，大概只占5.5MB的存储空间，对于切片应用来说，其它的解决方案倾向与受IO或是CPU的束缚，这些限制以及您存储查询这些数据的方式将迫使你将服务切片到更多的机器上。除非你采用Redis存储大量的多媒体文件，否则对于内存存储来说，这基本不是问题。对于应用来说，这就取决与你想要其受IO限制或是内存限制。

Redis did add support for virtual memory. However, this feature has been seen as a failure (by Redis' own developers) and its use has been deprecated.

Redis过去也支持虚拟内存。然而，这个特性已经被看作是一个失败（Redis官方的开发人员是这样认为的），所以也不推荐使用。

(On a side note, that 5.5MB file of Shakespeare's complete works can be compressed down to roughly 2MB. Redis doesn't do auto-compression but, since it treats values as bytes, there's no reason you can't trade processing time for RAM by compressing/decompressing the data yourself.)

（备注，5.5MB的莎士比亚全集可以完全压缩到大概2MB。Redis虽然不会自动压缩，但是既然都是以字节串的角度看待这些值，那么为什么不通过压缩/解压缩这些数据来换来内存处理速度的提升呢 ？）

## Putting It Together
## 汇总

We've touched on a number of high level topics. The last thing I want to do before diving into Redis is bring some of those topics together. Specifically, query limitations, data structures and Redis' way to store data in memory.

我们已经接触到了一些高阶主题。在我们继续深入Redis之前，我还想将这些主题汇总一下，具体指的是查询限制，数据结构，以及Redis的内存存储方式。

When you add those three things together you end up with something wonderful: speed. Some people think "Of course Redis is fast, everything's in memory." But that's only part of it. The real reason Redis shines versus other solutions is its specialized data structures.

当您将这三者结合在一起，您就会发现它们共同构筑的优势——速度。有人会说“Redis当然会快，所有东西都保存在内存中嘛。”但这只是其中部分原因。Redis真正超越同类方案的闪光指出，是在于其特殊的数据结构。

How fast? It depends on a lot of things - which commands you are using, the type of data, and so on. But Redis' performance tends to be measured in tens of thousands, or hundreds of thousands of operations **per second**. You can run `redis-benchmark` (which is in the same folder as the `redis-server` and `redis-cli`) to test it out yourself.

到底有多快？这取决于很多方面——您使用的是什么命令，什么类型的数据等等。但是Redis表现的计量单位，是**每秒**数万多数十万次操作。

I once changed code which used a traditional model to using Redis. A load test I wrote took over 5 minutes to finish using the relational model. It took about 150ms to complete in Redis. You won't always get that sort of massive gain, but it hopefully gives you an idea of what we are talking about.

我曾经将项目从从传统的数据模型移植到Redis上。我使用传统模型要超过5分钟才能完成的负载测试，在Redis下大概只花了150ms。一般情况下，您是很难获取如此巨幅的提升的。希望这个例子告诉您Redis所要呈现的性能。

It's important to understand this aspect of Redis because it impacts how you interact with it. Developers with an SQL background often work at minimizing the number of round trips they make to the database. That's good advice for any system, including Redis. However, given that we are dealing with simpler data structures, we'll sometimes need to hit the Redis server multiple times to achieve our goal. Such data access patterns can feel unnatural at first, but in reality it tends to be an insignificant cost compared to the raw performance we gain.

理解Redis这方面的性能对于我们与其进行交互的方式来说非常重要。拥有SQL背景的开发者通常要最大程度上的减少数据库中的环回。这对于包括Redis在内的所有系统来说都是好建议。但是，鉴于我们是要处理更加简单的数据结构。我们有时需要多次“破坏”Redis才能达到我们的目标。这样的数据处理方法，起初会感觉不自然，但实际情况是这比起我们的原始表现来说这些代价简直微不足道。

## In This Chapter
## 小结

Although we barely got to play with Redis, we did cover a wide range of topics. Don't worry if something isn't crystal clear - like querying. In the next chapter we'll go hands-on and any questions you have will hopefully answer themselves.

虽然只是简单体验了Redis，我们还是提到了许多主题。有些概念将得还不够透彻——比方说查询，不过不必担心。在下一章中，我们将继续深入，希望到时候所有的问题都能迎刃而解。

The important takeaways from this chapter are:
本章概要：

* Keys are strings which identify pieces of data (values)
* 键用以标定数据（值）的字符串

* Values are arbitrary byte arrays that Redis doesn't care about
* 值是二进制字节流，Redis并不关心其内容

* Redis exposes (and is implemented as) five specialized data structures
* Redis具备（并实现）五种特制的数据结构

* Combined, the above make Redis fast and easy to use, but not suitable for every scenario
* 结合在一起，所有以上特质让Redis快捷而且医用，但未必适用于所有场景。

# Chapter 2 - The Data Structures
# 数据结构

It's time to look at Redis' five data structures. We'll explain what each data structure is, what methods are available and what type of feature/data you'd use it for.

现在是时候看看Redis的五种数据结构了。我们将逐一介绍各种结构，以及其可用的方法，特性。

The only Redis constructs we've seen so far are commands, keys and values. So far, nothing about data structures has been concrete. When we used the `set` command, how did Redis know what data structure to use? It turns out that every command is specific to a data structure. For example when you use `set` you are storing the value in a string data structure. When you use `hset` you are storing it in a hash. Given the small size of Redis' vocabulary, it's quite manageable.

我们至今接触到的Redis结构只有命令、键和值，还没有具体的数据结构。当我调用“set”命令的时候，Redis如何知道我们要用那种数据结构呢？实际情况是每种命令都有其针对的数据结构。例如，当调用“set”的时候，您正将值保存到一个“string”类的数据结构中。当您调用“hset”的时候，值会保存到一个hash类型中。鉴于Redis的词汇表相当短小，这些还是很容易掌握的。

**[Redis' website](http://redis.io/commands) has great reference documentation. There's no point in repeating the work they've already done. We'll only cover the most important commands needed to understand the purpose of a data structure.**

**Redis的官网(http://redis.io/commands)上有完备的参考文档。重复他们已作的工作毫无意义。我们在这里只会介绍其中最重要的命令用于理解各种数据结构的目的。**

There's nothing more important than having fun and trying things out. You can always erase all the values in your database by entering `flushdb`, so don't be shy and try doing crazy things!

没有什么比动手实验更重要的了。您总可以通过调用`flushdb`命令清除数据库内所有数据。所以，想尝试什么疯狂的念头，就大胆去试吧。

## Strings

Strings are the most basic data structures available in Redis. When you think of a key-value pair, you are thinking of strings. Don't get mixed up by the name, as always, your value can be anything. I prefer to call them "scalars", but maybe that's just me.

Strings是Redis中最基础的数据结构了。当你在想一个键-值对的时候，你想的就是strings类型。请不要被它的名字所迷惑，就像之前所说，它的值可以是任何数据，我更倾向于称之为“标量”，不过可能只有我这么来。

We already saw a common use-case for strings, storing instances of objects by key. This is something that you'll make heavy use of:
我们已经看到最普通的strings用法，将对象实例用key来保存，以下这种用法你会大量用到：

	set users:leto "{name: leto, planet: dune, likes: [spice]}"

Additionally, Redis lets you do some common operations. For example `strlen <key>` can be used to get the length of a key's value; `getrange <key> <start> <end>` returns the specified range of a value; `append <key> <value>` appends the value to the existing value (or creates it if it doesn't exist already). Go ahead and try those out. This is what I get:

另外，Redis允许你进行一些常用的操作，比如，`strlen <key>`可以用户获取值的的长度；`getrange <key> <start> <end>`将返回指定区域内的值；`append <key> <value>`将追加value到已有的键值上（如果该键不存在就创建一个）。动手尝试，以下是我所得到的结果。

	> strlen users:leto
	(integer) 42

	> getrange users:leto 27 40
	"likes: [spice]"

	> append users:leto " OVER 9000!!"
	(integer) 54

Now, you might be thinking, that's great, but it doesn't make sense. You can't meaningfully pull a range out of JSON or append a value. You are right, the lesson here is that some of the commands, especially with the string data structure, only make sense given specific type of data.

现在，你可能会想，这不赖，但也没什么意义，你不能有意义地获取JSON的某段数据，或追加一个值。你是对的，这里只介绍了一些string数据结构相关的命令，只对这种特定的值有意义。

Earlier we learnt that Redis doesn't care about your values. Most of the time that's true. However, a few string commands are specific to some types or structure of values. As a vague example, I could see the above `append` and `getrange` commands being useful in some custom space-efficient serialization. As a more concrete example I give you the `incr`, `incrby`, `decr` and `decrby` commands. These increment or decrement the value of a string:

之前我们了解到Redis并不关系具体的值，大多数情况下这是对的，然而有些strings的命令是某些特定类型的值所专用的。作为一个定义相对模糊的类型，我可以发现像`append`、`getrange`命令在某天写特定场合下很有用，尤其是对于序列化的数据。接下来我介绍的`incr`、`incrby`、`decr`和`decrby`命令，用于对一个string值进行增减操作。

	> incr stats:page:about
	(integer) 1
	> incr stats:page:about
	(integer) 2

	> incrby ratings:video:12333 5
	(integer) 5
	> incrby ratings:video:12333 3
	(integer) 8

As you can imagine, Redis strings are great for analytics. Try incrementing `users:leto` (a non-integer value) and see what happens (you should get an error).

如您所想，Redis的strings类型适用于进行分析。试试自增一下`users:leto`（一个非整型数据）的值会出现什么情况（会返回一个错误）。

A more advanced example is the `setbit` and `getbit` commands. There's a [wonderful post](http://blog.getspool.com/2011/11/29/fast-easy-realtime-metrics-using-redis-bitmaps/) on how Spool uses these two commands to efficiently answer the question "how many unique visitors did we have today". For 128 million users a laptop generates the answer in less than 50ms and takes only 16MB of memory.

一个更加进阶的例子是`setbit`、`getbit`命令。有篇[博客](http://blog.getspool.com/2011/11/29/fast-easy-realtime-metrics-using-redis-bitmaps/)讲到Spool是如何应用这两条命令来有效回答“当日有多少不重复访客”这类的问题。对于128兆条用户记录，一台笔记本电脑大概能在50ms内计算出结构，而且值消耗16MB内存。

It isn't important that you understand how bitmaps work, or how Spool uses them, but rather to understand that Redis strings are more powerful than they initially seem. Still, the most common cases are the ones we gave above: storing objects (complex or not) and counters. Also, since getting a value by key is so fast, strings are often used to cache data.

现在急于去理解bitmaps的工作原理以及Spool是如何应用不是很重要，不如先对Redis的strings类型的强大更有概念些。而且，最重要的用法在上面已经给出来了，保存对象（不管复杂与否）以及计数器。另外，鉴于从键中获取值相当快速，strings常常用来当数据缓存。

## Hashes

Hashes are a good example of why calling Redis a key-value store isn't quite accurate. You see, in a lot of ways, hashes are like strings. The important difference is that they provide an extra level of indirection: a field. Therefore, the hash equivalents of `set` and `get` are:

Hashes（哈希表）是我们称Redis只是一个键-值存储器不太准确的好例证之一。可以看到，在很多方面，hashes和strings很相像。最重要的区别是，它还提供一个次级的指向：字段。所以对应与string的`set`和`get`，hash有：

	hset users:goku powerlevel 9000
	hget users:goku powerlevel

We can also set multiple fields at once, get multiple fields at once, get all fields and values, list all the fields or delete a specific field:

我们还能一次性对多个字段进行赋值，或取值。获取所有字段和值、所有字段、或删除一个特定字段。

	hmset users:goku race saiyan age 737
	hmget users:goku race powerlevel
	hgetall users:goku
	hkeys users:goku
	hdel users:goku age

As you can see, hashes give us a bit more control over plain strings. Rather than storing a user as a single serialized value, we could use a hash to get a more accurate representation. The benefit would be the ability to pull and update/delete specific pieces of data, without having to get or write the entire value.

可以看到，hashes向我们提供比简单的string更多的控制。不仅仅是用一个简单的序列化的值来保存用户实例，我们可以用hash实现更加精确的表达。好处是我们可以获取、更新/删除指定字段的数据，而无需获取或写入整个值。

Looking at hashes from the perspective of a well-defined object, such as a user, is key to understanding how they work. And it's true that, for performance reasons, more granular control might be useful. However, in the next chapter we'll look at how hashes can be used to organize your data and make querying more practical. In my opinion, this is where hashes really shine.

从一个完整定义对象（如user对象)的角度来看待hashes，是理解其工作方式的关键。也确实是这样，采用更加颗粒化的操作对于提升性能效果会有所帮助。然而，在下一节，我们可以看到hashes是如何用来组织数据，让查询变得更加可行。以我的偏见，这才是hash类型的闪光点所在。

## Lists

Lists let you store and manipulate an array of values for a given key. You can add values to the list, get the first or last value and manipulate values at a given index. Lists maintain their order and have efficient index-based operations. We could have a `newusers` list which tracks the newest registered users to our site:

Lists 让我们可以在一个键下存储和操作一组值。你可以向list添加值，获取list头或尾的值，或对某个特定下标的值进行操作。Lists会保持其内部顺序，并执行高效的基于序号的操作。我们可以使用一个名为`newusers`的list来跟踪我们网站上最新注册的用户：

	lpush newusers goku
	ltrim newusers 0 49

First we push a new user at the front of the list, then we trim it so that it only contains the last 50 users. This is a common pattern. `ltrim` is an O(N) operation, where N is the number of values we are removing. In this case, where we always trim after a single insert, it'll actually have a constant performance of O(1) (because N will always be equal to 1).

首先我们在List头部插入一个新用户，然后我们缩减这个list，使其只包含最新的50个用户。这是一种常用的用法，`ltrim`是一个O(N)的操作，N的值是我们要排除的元素数量，在本例中，我们在每次执行一个插入操作时就执行trim操作，所以实际上它的执行效率是O(1)，因为N的值始终为1。

This is also the first time that we are seeing a value in one key referencing a value in another. If we wanted to get the details of the last 10 users, we'd do the following combination:

这里我们第一次将一个键名作为value参数传入到一个list。如果想要获取最后10名用户的细节数据，我们可以使用以下命令组合：

	keys = redis.lrange('newusers', 0, 10)
	redis.mget(*keys.map {|u| "users:#{u}"})

The above is a bit of Ruby which shows the type of multiple roundtrips we talked about before.

这是一段Ruby代码，展现之前我们提到的多重引用。

Of course, lists aren't only good for storing references to other keys. The values can be anything. You could use lists to store logs or track the path a user is taking through a site. If you were building a game, you might use one to track a queued user actions.

当然，lists不仅仅擅于保存其它键的引用。其值可以是任何类型。您可以用lists来保存日志，记录用户在网站上的访问记录。如果你想设计一款游戏，你可以用list来记录用户的动作序列。

## Sets

Sets are used to store unique values and provide a number of set-based operations, like unions. Sets aren't ordered but they provide efficient value-based operations. A friend's list is the classic example of using a set:

Sets（集合）用于保存去重的值，并提供一些基于集合的操作，如unions。Sets内部无顺序科研，但是它能提供有效的基于值的操作。好友清单就是使用sets的典型应用。

	sadd friends:leto ghanima paul chani jessica
	sadd friends:duncan paul jessica alia

Regardless of how many friends a user has, we can efficiently tell (O(1)) whether userX is a friend of userY or not:

无论这个用户有多少朋友，我们都能非常高效（O(1)）地查询用户X是否是用户Y的朋友：

    sismember friends:leto jessica
	sismember friends:leto vladimir

Furthermore we can see whether two or more people share the same friends:
此外，我们还能查看两个或更多的用户中朋友清单中的重合部分：

	sinter friends:leto friends:duncan

and even store the result at a new key:
还能将结果保存到一个新的键中：

	sinterstore friends:leto_duncan friends:leto friends:duncan

Sets are great for tagging or tracking any other properties of a value for which duplicates don't make any sense (or where we want to apply set operations such as intersections and unions).

Set适用于标签、或用于跟踪一个值的其它属性，但这些属性不会重现重复内容的情况，或者我们可以讲其用于类似于重合查询以及unions类数据结构的情况。

## Sorted Sets

The last and most powerful data structure are sorted sets. If hashes are like strings but with fields, then sorted sets are like sets but with a score. The score provides sorting and ranking capabilities. If we wanted a ranked list of friends, we might do:

最后一个也是最强大的数据结构，就是sorted sets（排序集合）。如果Hash是带有字段的string，那么sorted sets就像是带有分值的sets。这些分值提供了分类以及排序的能力。如果我们要一个好友清单的排序结构，我们可以这么来：

	zadd friends:duncan 70 ghanima 95 paul 95 chani 75 jessica 1 vladimir

Want to find out how many friends `duncan` has with a score of 90 or over?
想要查询`duncan`的好友中有多少名在90分以上？

	zcount friends:duncan 90 100

How about figuring out `chani`'s rank?
若要查询`chani`的排位？

	zrevrank friends:duncan chani

We use `zrevrank` instead of `zrank` since Redis' default sort is from low to high (but in this case we are ranking from high to low). The most obvious use-case for sorted sets is a leaderboard system. In reality though, anything you want sorted by an some integer, and be able to efficiently manipulate based on that score, might be a good fit for a sorted set.

这里我们用`zrevrank`，而不是`zrank`，因为Redis的默认排序顺序为从低到高，但在本例中我们需要从高到低的逆序排列。sortred sets的一个最浅显的应用就是一个排位赛模型。从现实角度来说，所有你想用整形进行排序，并以此分值为基础进行操作的数据模型，可能都适用于sorted set。

## In This Chapter

That's a high level overview of Redis' five data structures. One of the neat things about Redis is that you can often do more than you first realize. There are probably ways to use string and sorted sets that no one has thought of yet. As long as you understand the normal use-case though, you'll find Redis ideal for all types of problems. Also, just because Redis exposes five data structures and various methods, don't think you need to use all of them. It isn't uncommon to build a feature while only using a handful of commands.

## 小结

本章大致介绍了Redis的五种数据结构。

# Chapter 3 - Leveraging Data Structures
# 效率分析

In the previous chapter we talked about the five data structures and gave some examples of what problems they might solve. Now it's time to look at a few more advanced, yet common, topics and design patterns.

之前我们大致介绍了五种数据结构，并给出了一些具体应用的例子。现在我们可以更进一步，谈一些深入的话题以及设计模式。

## Big O Notation
## 大O标记法

Throughout this book we've made references to the Big O notation in the form of O(n) or O(1). Big O notation is used to explain how something behaves given a certain number of elements. In Redis, it's used to tell us how fast a command is based on the number of items we are dealing with.

之前我们有提到大O标记法的概念，无论是O(N)还是O(1)，大O标记法是用于解释对特定数量的元素执行操作时的复杂度指标。在Redis中，这个概念用于告诉我们基于我们要处理的元素数量，特定的操作需要执行多长时间。
Redis documentation tells us the Big O notation for each of its commands. It also tells us what the factors are that influence the performance. Let's look at some examples.

Redis文档对每条命令，都用大O标记法介绍其复杂度，还介绍了影响其效率的因素。我们看看以下例子。

The fastest anything can be is O(1) which is a constant. Whether we are dealing with 5 items or 5 million, you'll get the same performance. The `sismember` command, which tells us if a value belongs to a set, is O(1). `sismember` is a powerful command, and its performance characteristics are a big reason for that. A number of Redis commands are O(1).

最快的复杂度莫过于是O(1)，它是个常量。无论是我们是要处理五个元素，或是五百万个元素，执行的速度是一样。“sismember”告诉我们一个值是否被包含在一个set集合中，它的复杂度就是O(1)。“sismember”之所以强大和它的执行效率是分不开的。有一部分Redis指令的复杂度就是O(1)。

Logarithmic, or O(log(N)), is the next fastest possibility because it needs to scan through smaller and smaller partitions. Using this type of divide and conquer approach, a very large number of items quickly gets broken down in a few iterations. `zadd` is a O(log(N)) command, where N is the number of elements already in the set.

指数级，O(log(N))，是第二快的复杂度，因为它所需要扫描的分区越来越小。使用这种分部求解的方法，一个巨大的元素集合可以快速地被迭代分解越来越小的集合。"zadd"就是一个O(log(N))的指令，其中N的值是已有集合中的元素个数。

Next we have linear commands, or O(N). Looking for a non-indexed column in a table is an O(N) operation. So is using the `ltrim` command. However, in the case of `ltrim`, N isn't the number of elements in the list, but rather the elements being removed. Using `ltrim` to remove 1 item from a list of millions will be faster than using `ltrim` to remove 10 items from a list of thousands. (Though they'll probably both be so fast that you wouldn't be able to time it.)

接下来就是线级别，O(N)，如查找一个表中未索引的列。“ltrim”就是这样的命令，但也有一点特殊，N并不是list中所有元素的个数，而是需要移除的元素个数。从一个百万级的list中移除1个元素的速度要比从一个千级的List中移除10个元素的速度要快。（不过它们两个都太快了，以至于你根本没法测量。）

`zremrangebyscore` which removes elements from a sorted set with a score between a minimum and a maximum value has a complexity of O(log(N)+M). This makes it a mix. By reading the documentation we see that N is the number of total elements in the set and M is the number of elements to be removed. In other words, the number of elements that'll get removed is probably going to be more significant, in terms of performance, than the total number of elements in the set.

“zremrangebyscore”命令，是从一个sorted set中移除分值在参数minimum和maximum之间的元素，其复杂度为O(log(N)+M)。这是一种混合表达法。通过阅读文档，我们了解到，N值得集合的元素总数，M值为要移除的元素个数。换言之，要移除的元素个数可能比集合的元素总数对于效率的影响更加显著。

The `sort` command, which we'll discuss in greater detail in the next chapter has a complexity of O(N+M*log(M)). From its performance characteristic, you can probably tell that this is one of Redis' most complex commands.

“sort”命令，将在下一章作更加详尽的介绍，它的复杂度为O(N+M*log(M))，可以从它的复杂度属性大概可以看出这估计是Redis最为复杂的指令了。

There are a number of other complexities, the two remaining common ones are O(N^2) and O(C^N). The larger N is, the worse these perform relative to a smaller N. None of Redis' commands have this type of complexity.

还有其它的复杂度，还有两个常用的，分别是 O(N^2)和O(C^N)。N值越大，执行效率就越低。不过Redis的命令中没有复杂度达到这样的。

It's worth pointing out that the Big O notation deals with the worst case. When we say that something takes O(N), we might actually find it right away or it might be the last possible element.

值得指出的是，大O标记法通常指的是最糟糕的情况。当我们说有个运算复杂度是O(N)，我们可能实际上一下子就求得结果，也有可能要算最后一次才能求得。

## Pseudo Multi Key Queries
## 伪多键查询

A common situation you'll run into is wanting to query the same value by different keys. For example, you might want to get a user by email (for when they first log in) and also by id (after they've logged in). One horrible solution is to duplicate your user object into two string values:

我们经常会遇到一个情况，就是要从多个键中查询出相同的值。例如，你可能要通过Email查到用户（当他们首次登录时），或者通过id进行查询用户信息（当他们已经登录后），有一种糟糕的解决方法就是，在两个string副本中都保存一样的用户信息。

	set users:leto@dune.gov "{id: 9001, email: 'leto@dune.gov', ...}"
	set users:9001 "{id: 9001, email: 'leto@dune.gov', ...}"

This is bad because it's a nightmare to manage and it takes twice the amount of memory.

这种做法很糟糕，对于管理来说是个噩梦，同时消耗了两倍的内存。

It would be nice if Redis let you link one key to another, but it doesn't (and it probably never will). A major driver in Redis' development is to keep the code and API clean and simple. The internal implementation of linking keys (there's a lot we can do with keys that we haven't talked about yet) isn't worth it when you consider that Redis already provides a solution: hashes.

如果Redis可以让一个键链接到另一个键就好了，但是它并没有这么做（大概以后也不准备这样）。Redis开发的一个核心理念就是要保持API的简洁。当您意识到Redis已经提供了一个解决方案：hashed，您就会发现发现链接键并不划算（键的用法有很多我们还没提到）。

Using a hash, we can remove the need for duplication:
通过hash，我们一个除去复制数据的需要：

	set users:9001 "{id: 9001, email: leto@dune.gov, ...}"
	hset users:lookup:email leto@dune.gov 9001

What we are doing is using the field as a pseudo secondary index and referencing the single user object. To get a user by id, we issue a normal `get`:

我们这里要做的是将一个字段作为伪附属索引，并将其引用到一个user对象。要通过id获取user，我们只需要执行简单的`get`：

	get users:9001

To get a user by email, we issue an `hget` followed by a `get` (in Ruby):
要通过email获取user，我们只需要在`get`之后执行`hget`（Ruby实现）：

	id = redis.hget('users:lookup:email', 'leto@dune.gov')
	user = redis.get("users:#{id}")

This is something that you'll likely end up doing often. To me, this is where hashes really shine, but it isn't an obvious use-case until you see it.

这就是您将在Redis中经常会用到的做法。对于我来说，这正是hashed真正闪光的地方，但如果没有亲眼见到的话，您不会觉得这是一个很明显的用例。

## References and Indexes
## 引用与索引

We've seen a couple examples of having one value reference another. We saw it when we looked at our list example, and we saw it in the section above when using hashes to make querying a little easier. What this comes down to is essentially having to manually manage your indexes and references between values. Being honest, I think we can say that's a bit of a downer, especially when you consider having to manage/update/delete these references manually. There is no magic solution to solving this problem in Redis.

We already saw how sets are often used to implement this type of manual index:

	sadd friends:leto ghanima paul chani jessica

Each member of this set is a reference to a Redis string value containing details on the actual user. What if `chani` changes her name, or deletes her account? Maybe it would make sense to also track the inverse relationships:

	sadd friends_of:chani leto paul

Maintenance cost aside, if you are anything like me, you might cringe at the processing and memory cost of having these extra indexed values. In the next section we'll talk about ways to reduce the performance cost of having to do extra round trips (we briefly talked about it in the first chapter).

If you actually think about it though, relational databases have the same overhead. Indexes take memory, must be scanned or ideally seeked and then the corresponding records must be looked up. The overhead is neatly abstracted away (and they  do a lot of optimizations in terms of the processing to make it very efficient).

Again, having to manually deal with references in Redis is unfortunate. But any initial concerns you have about the performance or memory implications of this should be tested. I think you'll find it a non-issue.

## Round Trips and Pipelining

We already mentioned that making frequent trips to the server is a common pattern in Redis. Since it is something you'll do often, it's worth taking a closer look at what features we can leverage to get the most out of it.

First, many commands either accept one or more set of parameters or have a sister-command which takes multiple parameters. We saw `mget` earlier, which takes multiple keys and returns the values:

	keys = redis.lrange('newusers', 0, 10)
	redis.mget(*keys.map {|u| "users:#{u}"})

Or the `sadd` command which adds 1 or more members to a set:

	sadd friends:vladimir piter
	sadd friends:paul jessica leto "leto II" chani

Redis also supports pipelining. Normally when a client sends a request to Redis it waits for the reply before sending the next request. With pipelining you can send a number of requests without waiting for their responses. This reduces the networking overhead and can result in significant performance gains.

It's worth noting that Redis will use memory to queue up the commands, so it's a good idea to batch them. How large a batch you use will depend on what commands you are using, and more specifically, how large the parameters are. But, if you are issuing commands against ~50 character keys, you can probably batch them in thousands or tens of thousands.

Exactly how you execute commands within a pipeline will vary from driver to driver. In Ruby you pass a block to the `pipelined` method:

	redis.pipelined do
	  9001.times do
		redis.incr('powerlevel')
	  end
	end

As you can probably guess, pipelining can really speed up a batch import!

## Transactions

Every Redis command is atomic, including the ones that do multiple things. Additionally, Redis has support for transactions when using multiple commands.

You might not know it, but Redis is actually single-threaded, which is how every command is guaranteed to be atomic. While one command is executing, no other command will run. (We'll briefly talk about scaling in a later chapter.) This is particularly useful when you consider that some commands do multiple things. For example:

`incr` is essentially a `get` followed by a `set`

`getset` sets a new value and returns the original

`setnx` first checks if the key exists, and only sets the value if it does not

Although these commands are useful, you'll inevitably need to run multiple commands as an atomic group. You do so by first issuing the `multi` command, followed by all the commands you want to execute as part of the transaction, and finally executing `exec` to actually execute the commands or `discard` to throw away, and not execute the commands. What guarantee does Redis make about transactions?

* The commands will be executed in order

* The commands will be executed as a single atomic operation (without another client's command being executed halfway through)

* That either all or none of the commands in the transaction will be executed

You can, and should, test this in the command line interface. Also note that there's no reason why you can't combine pipelining and transactions.

	multi
	hincrby groups:1percent balance -9000000000
	hincrby groups:99percent balance 9000000000
	exec

Finally, Redis lets you specify a key (or keys) to watch and conditionally apply a transaction if the key(s) changed. This is used when you need to get values and execute code based on those values, all in a transaction. With the code above, we wouldn't be able to implement our own `incr` command since they are all executed together once `exec` is called. From code, we can't do:

	redis.multi()
	current = redis.get('powerlevel')
	redis.set('powerlevel', current + 1)
	redis.exec()

That isn't how Redis transactions work. But, if we add a `watch` to `powerlevel`, we can do:

	redis.watch('powerlevel')
	current = redis.get('powerlevel')
	redis.multi()
	redis.set('powerlevel', current + 1)
	redis.exec()

If another client changes the value of `powerlevel` after we've called `watch` on it, our transaction will fail. If no client changes the value, the set will work. We can execute this code in a loop until it works.

## Keys Anti-Pattern

In the next chapter we'll talk about commands that aren't specifically related to data structures. Some of these are administrative or debugging tools. But there's one I'd like to talk about in particular: the `keys` command. This command takes a pattern and finds all the matching keys. This command seems like it's well suited for a number of tasks, but it should never be used in production code. Why? Because it does a linear scan through all the keys looking for matches. Or, put simply, it's slow.

How do people try and use it? Say you are building a hosted bug tracking service. Each account will have an `id` and you might decide to store each bug into a string value with a key that looks like `bug:account_id:bug_id`. If you ever need to find all of an account's bugs (to display them, or maybe delete them if they delete their account), you might be tempted (as I was!) to use the `keys` command:

	keys bug:1233:*

The better solution is to use a hash. Much like we can use hashes to provide a way to expose secondary indexes, so too can we use them to organize our data:

	hset bugs:1233 1 "{id:1, account: 1233, subject: '...'}"
	hset bugs:1233 2 "{id:2, account: 1233, subject: '...'}"

To get all the bug ids for an account we simply call `hkeys bugs:1233`. To delete a specific bug we can do `hdel bugs:1233 2` and to delete an account we can delete the key via `del bugs:1233`.


## In This Chapter

This chapter, combined with the previous one, has hopefully given you some insight on how to use Redis to power real features. There are a number of other patterns you can use to build all types of things, but the real key is to understand the fundamental data structures and to get a sense for how they can be used to achieve things beyond your initial perspective.

# Chapter 4 - Beyond The Data Structures

While the five data structures form the foundation of Redis, there are other commands which aren't data structure specific. We've already seen a handful of these: `info`, `select`, `flushdb`, `multi`, `exec`, `discard`, `watch` and `keys`. This chapter will look at some of the other important ones.

## Expiration

Redis allows you to mark a key for expiration. You can give it an absolute time in the form of a Unix timestamp (seconds since January 1, 1970) or a time to live in seconds. This is a key-based command, so it doesn't matter what type of data structure the key represents.

	expire pages:about 30
	expireat pages:about 1356933600

The first command will delete the key (and associated value) after 30 seconds. The second will do the same at 12:00 a.m. December 31st, 2012.

This makes Redis an ideal caching engine. You can find out how long an item has to live until via the `ttl` command and you can remove the expiration on a key via the `persist` command:

	ttl pages:about
	persist pages:about

Finally, there's a special string command, `setex` which lets you set a string and specify a time to live in a single atomic command (this is more for convenience than anything else):

	setex pages:about 30 '<h1>about us</h1>....'

## Publication and Subscriptions

Redis lists have an `blpop` and `brpop` command which returns and removes the first (or last) element from the list or blocks until one is available. These can be used to power a simple queue.

Beyond this, Redis has first-class support for publishing messages and subscribing to channels. You can try this out yourself by opening a second `redis-cli` window. In the first window subscribe to a channel (we'll call it `warnings`):

	subscribe warnings

The reply is the information of your subscription. Now, in the other window, publish a message to the `warnings` channel:

	publish warnings "it's over 9000!"

If you go back to your first window you should have received the message to the `warnings` channel.

You can subscribe to multiple channels (`subscribe channel1 channel2 ...`), subscribe to a pattern of channels (`psubscribe warnings:*`) and use the `unsubscribe` and `punsubscribe` commands to stop listening to one or more channels, or a channel pattern.

Finally, notice that the `publish` command returned the value 1. This indicates the number of clients that received the message.


## Monitor and Slow Log

The `monitor` command lets you see what Redis is up to. It's a great debugging tool that gives you insight into how your application is interacting with Redis. In one of your two redis-cli windows (if one is still subscribed, you can either use the `unsubscribe` command or close the window down and re-open a new one) enter the `monitor` command. In the other, execute any other type of command (like `get` or `set`). You should see those commands, along with their parameters, in the first window.

You should be wary of running monitor in production, it really is a debugging and development tool. Aside from that, there isn't much more to say about it. It's just a really useful tool.

Along with `monitor`, Redis has a `slowlog` which acts as a great profiling tool. It logs any command which takes longer than a specified number of **micro**seconds. In the next section we'll briefly cover how to configure Redis, for now you can configure Redis to log all commands by entering:

	config set slowlog-log-slower-than 0

Next, issue a few commands. Finally you can retrieve all of the logs, or the most recent logs via:

	slowlog get
	slowlog get 10

You can also get the number of items in the slow log by entering `slowlog len`

For each command you entered you should see four parameters:

* An auto-incrementing id

* A Unix timestamp for when the command happened

* The time, in microseconds, it took to run the command

* The command and its parameters

The slow log is maintained in memory, so running it in production, even with a low threshold, shouldn't be a problem. By default it will track the last 1024 logs.

## Sort

One of Redis' most powerful commands is `sort`. It lets you sort the values within a list, set or sorted set (sorted sets are ordered by score, not the members within the set). In its simplest form, it allows us to do:

	rpush users:leto:guesses 5 9 10 2 4 10 19 2
	sort users:leto:guesses

Which will return the values sorted from lowest to highest. Here's a more advanced example:

	sadd friends:ghanima leto paul chani jessica alia duncan
	sort friends:ghanima limit 0 3 desc alpha

The above command shows us how to page the sorted records (via `limit`), how to return the results in descending order (via `desc`) and how to sort lexicographically instead of numerically (via `alpha`).

The real power of `sort` is its ability to sort based on a referenced object. Earlier we showed how lists, sets and sorted sets are often used to reference other Redis objects. The `sort` command can dereference those relations and sort by the underlying value. For example, say we have a bug tracker which lets users watch issues. We might use a set to track the issues being watched:

	sadd watch:leto 12339 1382 338 9338

It might make perfect sense to sort these by id (which the default sort will do), but we'd also like to have these sorted by severity. To do so, we tell Redis what pattern to sort by. First, let's add some more data so we can actually see a meaningful result:

	set severity:12339 3
	set severity:1382 2
	set severity:338 5
	set severity:9338 4

To sort the bugs by severity, from highest to lowest, you'd do:

	sort watch:leto by severity:* desc

Redis will substitute the `*` in our pattern (identified via `by`) with the values in our list/set/sorted set. This will create the key name that Redis will query for the actual values to sort by.

Although you can have millions of keys within Redis, I think the above can get a little messy. Thankfully `sort` can also work on hashes and their fields. Instead of having a bunch of top-level keys you can leverage hashes:

	hset bug:12339 severity 3
	hset bug:12339 priority 1
	hset bug:12339 details "{id: 12339, ....}"

	hset bug:1382 severity 2
	hset bug:1382 priority 2
	hset bug:1382 details "{id: 1382, ....}"

	hset bug:338 severity 5
	hset bug:338 priority 3
	hset bug:338 details "{id: 338, ....}"

	hset bug:9338 severity 4
	hset bug:9338 priority 2
	hset bug:9338 details "{id: 9338, ....}"

Not only is everything better organized, and we can sort by `severity` or `priority`, but we can also tell `sort` what field to retrieve:

	sort watch:leto by bug:*->priority get bug:*->details

The same value substitution occurs, but Redis also recognizes the `->` sequence and uses it to look into the specified field of our hash. We've also included the `get` parameter, which also does the substitution and field lookup, to retrieve bug details.

Over large sets, `sort` can be slow. The good news is that the output of a `sort` can be stored:

	sort watch:leto by bug:*->priority get bug:*->details store watch_by_priority:leto

Combining the `store` capabilities of `sort` with the expiration commands we've already seen makes for a nice combo.

## In This Chapter

This chapter focused on non-data structure-specific commands. Like everything else, their use is situational. It isn't uncommon to build an app or feature that won't make use of expiration, publication/subscription and/or sorting. But it's good to know that they are there. Also, we only touched on some of the commands. There are more, and once you've digested the material in this book it's worth going through the [full list](http://redis.io/commands).

# Chapter 5 - Lua Scripting

Redis 2.6 includes a built-in Lua interpreter which developers can leverage to write more advanced queries to be executed within Redis. It wouldn't be wrong of you to think of this capability much like you might view stored procedures available in most relational databases.

The most difficult aspect of mastering this feature is learning Lua. Thankfully, Lua is similar to most general purpose languages, is well documented, has an active community and is useful to know beyond Redis scripting. This chapter won't cover Lua in any detail; but the few examples we look at should hopefully serve as a simple introduction.

## Why?

Before looking at how to use Lua scripting, you might be wondering why you'd want to use it. Many developers dislike traditional stored procedures, is this any different? The short answer is no. Improperly used, Redis' Lua scripting can result in harder to test code, business logic tightly coupled with data access or even duplicated logic.

Properly used however, it's a feature that can simplify code and improve performance. Both of these benefits are largely achieved by grouping multiple commands, along with some simple logic, into a custom-build cohesive function. Code is made simpler because each invocation of a Lua script is run without interruption and thus provides a clean way to create your own atomic commands (essentially eliminating the need to use the cumbersome `watch` command). It can improve performance by removing the need to return intermediary results - the final output can be calculated within the script.

The examples in the following sections will better illustrate these points.

## Eval

The `eval` command takes a Lua script (as a string), the keys we'll be operating against, and an optional set of arbitrary arguments. Let's look at a simple example (executed from Ruby, since running multi-line Redis commands from its command-line tool isn't fun):

    script = <<-eos
      local friend_names = redis.call('smembers', KEYS[1])
      local friends = {}
      for i = 1, #friend_names do
        local friend_key = 'user:' .. friend_names[i]
        local gender = redis.call('hget', friend_key, 'gender')
        if gender == ARGV[1] then
          table.insert(friends, redis.call('hget', friend_key, 'details'))
        end
      end
      return friends
    eos
    Redis.new.eval(script, ['friends:leto'], ['m'])

The above code gets the details for all of Leto's male friends. Notice that to call Redis commands within our script we use the `redis.call("command", ARG1, ARG2, ...)` method.

If you are new to Lua, you should go over each line carefully. It might be useful to know that `{}` creates an empty `table` (which can act as either an array or a dictionary), `#TABLE` gets the number of elements in the TABLE, and `..` is used to concatenate strings.

`eval` actually take 4 parameters. The second parameter should actually be the number of keys; however the Ruby driver automatically creates this for us. Why is this needed? Consider how the above looks like when executed from the CLI:
  
    eval "....." "friends:leto" "m"
    vs
    eval "....." 1 "friends:leto" "m"

In the first (incorrect) case, how does Redis know which of the parameters are keys and which are simply arbitrary arguments? In the second case, there is no ambiguity.

This brings up a second question: why must keys be explicitly listed? Every command in Redis knows, at execution time, which keys are going to needed. This will allow future tools, like Redis Cluster, to  distribute requests amongst multiple Redis servers. You might have spotted that our above example actually reads from keys dynamically (without having them passed to `eval`). An `hget` is issued on all of Leto's male friends. That's because the need to list keys ahead of time is more of a suggestion than a hard rule. The above code will run fine in a single-instance setup, or even with replication, but won't in the yet-released Redis Cluster.

## Script Management

Even though scripts executed via `eval` are cached by Redis, sending the body every time you want to execute something isn't ideal. Instead, you can register the script with Redis and execute it's key. To do this you use the `script load` command, which returns the SHA1 digest of the script:

    redis = Redis.new
    script_key = redis.script(:load, "THE_SCRIPT")

Once we've loaded the script, we can use `evalsha` to execute it:

    redis.evalsha(script_key, ['friends:leto'], ['m'])

`script kill`, `script flush` and `script exists` are the other commands that you can use to manage Lua scripts. They are used to kill a running script, removing all scripts from the internal cache and seeing if a script already exists within the cache.

## Libraries

Redis' Lua implementation ships with a handful of useful libraries. While `table.lib`, `string.lib` and `math.lib` are quite useful, for me, `cjson.lib` is worth singling out. First, if you find yourself having to pass multiple arguments to a script, it might be cleaner to pass it as JSON:

    redis.evalsha ".....", [KEY1], [JSON.fast_generate({gender: 'm', ghola: true})]

Which you could then deserialize within the Lua script as:

    local arguments = cjson.decode(ARGV[1])

Of course, the JSON library can also be used to parse values stored in Redis itself. Our above example could potentially be rewritten as such:

      local friend_names = redis.call('smembers', KEYS[1])
      local friends = {}
      for i = 1, #friend_names do
        local friend_raw = redis.call('get', 'user:' .. friend_names[i])
        local friend_parsed = cjson.decode(friend_raw)
        if friend_parsed.gender == ARGV[1] then
          table.insert(friends, friend_raw)
        end
      end
      return friends

Instead of getting the gender from specific hash field, we could get it from the stored friend data itself. (This is a much slower solution, and I personally prefer the original, but it does show what's possible).

## Atomic

Since Redis is single-threaded, you don't have to worry about your Lua script being interrupted by another Redis command. One of the most obvious benefits of this is that keys with a TTL won't expire half-way through execution. If a key is present at the start of the script, it'll be present at any point thereafter - unless you delete it.

## Administration

The next chapter will talk about Redis administration and configuration in more detail. For now, simply know that the `lua-time-limit` defines how long a Lua script is allowed to execute before being terminated. The default is generous 5 seconds. Consider lowering it.

## In This Chapter

This chapter introduced Redis' Lua scripting capabilities. Like anything, this feature can be abused. However, used prudently in order to implement your own custom and focused commands, it won't only simplify your code, but will likely improve performance. Lua scripting is like almost every other Redis feature/command: you make limited, if any, use of it at first only to find yourself using it more and more every day. 

# Chapter 6 - Administration

Our last chapter is dedicated to some of the administrative aspects of running Redis. In no way is this a comprehensive guide on Redis administration. At best we'll answer some of the more basic questions new users to Redis are most likely to have.

## Configuration

When you first launched the Redis server, it warned you that the `redis.conf` file could not be found. This file can be used to configure various aspects of Redis. A well-documented `redis.conf` file is available for each release of Redis. The sample file contains the default configuration options, so it's useful to both understand what the settings do and what their defaults are. You can find it at <https://github.com/antirez/redis/raw/2.4.6/redis.conf>.

**This is the config file for Redis 2.4.6. You should replace "2.4.6" in the above URL with your version. You can find your version by running the `info` command and looking at the first value.**

Since the file is well-documented, we won't be going over the settings.

In addition to configuring Redis via the `redis.conf` file, the `config set` command can be used to set individual values. In fact, we already used it when setting the `slowlog-log-slower-than` setting to 0.

There's also the `config get` command which displays the value of a setting. This command supports pattern matching. So if we want to display everything related to logging, we can do:

	config get *log*

## Authentication

Redis can be configured to require a password. This is done via the `requirepass` setting (set through either the `redis.conf` file or the `config set` command). When `requirepass` is set to a value (which is the password to use), clients will need to issue an `auth password` command.

Once a client is authenticated, they can issue any command against any database. This includes the `flushall` command which erases every key from every database. Through the configuration, you can rename commands to achieve some security through obfuscation:

	rename-command CONFIG 5ec4db169f9d4dddacbfb0c26ea7e5ef
	rename-command FLUSHALL 1041285018a942a4922cbf76623b741e

Or you can disable a command by setting the new name to an empty string.

## Size Limitations

As you start using Redis, you might wonder "how many keys can I have?" You might also wonder how many fields can a hash have (especially when you use it to organize your data), or how many elements can lists and sets have? Per instance, the practical limits for all of these is in the hundreds of millions.


## Replication

Redis supports replication, which means that as you write to one Redis instance (the master), one or more other instances (the slaves) are kept up-to-date by the master. To configure a slave you use either the `slaveof` configuration setting or the `slaveof` command (instances running without this configuration are or can be masters).

Replication helps protect your data by copying to different servers. Replication can also be used to improve performance since reads can be sent to slaves. They might respond with slightly out of date data, but for most apps that's a worthwhile tradeoff.

Unfortunately, Redis replication doesn't yet provide automated failover. If the master dies, a slave needs to be manually promoted. Traditional high-availability tools that use heartbeat monitoring and scripts to automate the switch are currently a necessary headache if you want to achieve some sort of high availability with Redis.

## Backups

Backing up Redis is simply a matter of copying Redis' snapshot to whatever location you want (S3, FTP, ...). By default Redis saves its snapshot to a file named `dump.rdb`. At any point in time, you can simply `scp`, `ftp` or `cp` (or anything else) this file.

It isn't uncommon to disable both snapshotting and the append-only file (aof) on the master and let a slave take care of this. This helps reduce the load on the master and lets you set more aggressive saving parameters on the slave without hurting overall system responsiveness.

## Scaling and Redis Cluster

Replication is the first tool a growing site can leverage. Some commands are more expensive than others (`sort` for example) and offloading their execution to a slave can keep the overall system responsive to incoming queries.

Beyond this, truly scaling Redis comes down to distributing your keys across multiple Redis instances (which could be running on the same box, remember, Redis is single-threaded). For the time being, this is something you'll need to take care of (although a number of Redis drivers do provide consistent-hashing algorithms). Thinking about your data in terms of horizontal distribution isn't something we can cover in this book. It's also something you probably won't have to worry about for a while, but it's something you'll need to be aware of regardless of what solution you use.

The good news is that work is under way on Redis Cluster. Not only will this offer horizontal scaling, including rebalancing, but it'll also provide automated failover for high availability.

High availability and scaling is something that can be achieved today, as long as you are willing to put the time and effort into it. Moving forward, Redis Cluster should make things much easier.

## In This Chapter

Given the number of projects and sites using Redis already, there can be no doubt that Redis is production-ready, and has been for a while. However, some of the tooling, especially around security and availability is still young. Redis Cluster, which we'll hopefully see soon, should help address some of the current management challenges.

# Conclusion

In a lot of ways, Redis represents a simplification in the way we deal with data. It peels away much of the complexity and abstraction available in other systems. In many cases this makes Redis the wrong choice. In others it can feel like Redis was custom-built for your data.

Ultimately it comes back to something I said at the very start: Redis is easy to learn. There are many new technologies and it can be hard to figure out what's worth investing time into learning. When you consider the real benefits Redis has to offer with its simplicity, I sincerely believe that it's one of the best investments, in terms of learning, that you and your team can make.

