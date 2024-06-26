# 智能合约开发指南

### 目录

- [1. 选择智能合约语言](#1-选择智能合约语言)
    - [1.1 Solidity](#11-solidity)
    - [1.2 Vyper](#12-vyper)
    - [1.3 Move](#13-move)
    - [1.4 Rust](#14-rust)
- [2. 部署和测试框架](#2-部署和测试框架)
    - [2.1 概览](#21-概览)
    - [2.2 Remix](#22-Remix)
    - [2.3 Truffle](#23-Truffle)
    - [2.4 Hardhat](#24-hardhat)
    - [2.5 其他框架](#25-其他框架)
- [3. 前端工具](#3-前端工具)
    - [3.1 入门](#31-入门)
    - [3.2 Web3.js/Ethers.js](#32-web3jsethersjs)
    - [3.3 脚手架](#33-脚手架)
    - [3.4 Moralis](#34-moralis)
- [4. 钱包](#4-钱包)
    - [4.1 小狐狸钱包（MetaMask）](#41-小狐狸钱包MetaMask)
    - [4.2 多签钱包](#42-多签钱包)
    - [4.3 冷钱包](#43-冷钱包)
- [5. 区块浏览器](#5-区块浏览器)
- [6. 测试网与水龙头](#6-测试网与水龙头)
- [7. Web3基础设施](#7-Web3基础设施)


## 前言

从底层的区块链基础设施到建立在其之上的应用层的智能合约生态，Web3领域已经发展的相当之快。基于智能合约，我们可以构建出各种各样的dApp（去中心化应用），
比如DeFi、GameFi、NFT、GameFi甚至是这两年兴起的SocialFi类应用。列举出的每一类dApp都在各自的领域内大放异彩，造就了整个Web3领域的蓬勃发展的繁荣景象。

当你熟悉智能合约开发之后，不论你想要开发任何一种（上面列出的）dApp，都已经拥有50%的基础优势，剩下的50%就是需要熟悉对应dApp领域的业务知识，下面就一起来看看智能合约开发的学习路线。

需要特别说明的是，本文注重实用性，不会过多介绍相关工具的历史，这方面读者可自行查询。

## 1. 选择智能合约语言

合约编程语言是智能合约开发者最基本的部分，你至少应该掌握一种才能编写智能合约。合约语言通常不是传统的编程语言（如C/C++，Python等）， 为了保证合约代码在任何一个区块链节点上都能够得到一个确定的执行结果，
必须要求合约不能访问外部世界（如进行HTTP连接或操作文件），早期的区块链开发者们设计出了专为编写合约的编程语言，如Solidity、Vyper，
后来又诞生了一些新的合约语言如Move或Rust（但包含一些使用限制）。好消息是这些语言都大量借鉴了传统编程语言的语法，如Solidity借鉴JavaScript、Vyper借鉴Python，这使得成为一名合约开发者的学习曲线平坦了一些。

### 1.1 Solidity

首先，一个不用过多思考的选择是Solidity，因为目前90%的智能合约都是Solidity写的。Solidity算是最早也是最流行的面向对象的高级静态语言，最初2014年是为以太坊EVM量身设计的，
后来又出现了很多兼容以太坊EVM的区块链平台（如Ethereum、Avalanche、Moonbeam、Polygon、BSC），所以现在Solidity也可以运行在其他那些兼容EVM的区块链上。 在目前排名前十的 [Defi项目][0]
中，有九个使用Solidity作为他们的主要编程语言。

Solidity发展至今已经快十年，生态内已经有大量优秀的开发工具可供使用，包括第三方库以及IDE等（后面介绍）。另外，在EVM上运行的比Solidity更原生的语言是汇编语言Yul，进阶Solidity时你会了解到Solidity与Yul通过内联交互以提高性能的应用。

需要注意的是，Solidity在语法设计上存在一些缺陷，当然，这些年不断的被改进，在易用性和安全性上已经得到了极大的提升。

对于Solidity的学习，这里强烈推荐本仓库主页中列出的书籍 [智能合约技术与开发](https://item.jd.com/10057770151476.html)
，且在本仓库中也存放有笔者对该书的[代码笔记](./test_solidity/basic_exercises) 。

### 1.2 Vyper

Vyper是另一种与EVM兼容（可编译为像Solidity一样的EVM字节码）且相比Solidity更注重安全性的合约语言，它与Python的语法非常相似，但相比Python去掉了许多不必要的特性（如类继承、函数重载、运算符重载等），
减少特性可以语言变得简单，也减少了出错的机会。

另外，Vyper 还旨在让任何人尽可能难以编写误导性代码。读者（即审核员）的简单性比作者（即开发人员）的简单性更重要。这样，将更容易识别智能合约或去中心化应用程序 (dApp) 中的恶意代码。

需要注意的是，Vyper不是Solidity的完全替代品，而是一种在需要最高安全级别时使用的语言。用 Vyper 编写的项目示例包括 Uniswap v1、Curve.fi 和第一个 ETH 2.0 存款合约。

### 1.3 Move

Move创建于2019年，是一门相对Solidity和Vyper来说较难掌握的合约语言，它基于Rust改写，最初是为 Meta 的 Diem 区块链项目而开发的，在 Diem 项目解散之后， 其创始团队出走分别创立的 Aptos
与Sui，也将 Move 作为核心编程语言。

Move的主要特点是面向资产编程（资源是一等公民）、安全（继承了Rust诸多安全特性）以及模块化（模块可以迭代）。

相对来说，Move 语言目前还十分年轻，缺乏大规模的工程化验证，并且其开发链尚不完善，合约规范也没有形成，所以建议只作为兴趣了解。

### 1.4 Rust

Rust 最初由 Mozilla 员工 Graydon Hoare 在 2006 年设计和发布，是一种为性能和安全性，尤其是安全并发性而设计的语言，它在语法上与 C++ 相似。 Rust
并不是一开始就为了智能合约而设计，而是作为一门传统的力求高安全性的高级语言而存在，由于其在安全性上的优势十分契合智能合约的应用场景， 所以人们选择直接将其引入区块链领域。

目前，Rust在区块链各领域已经被广泛应用，如区块链基础设施建设（Layer 1）、合约编程（Layer 2）等。目前将 Rust 语言作为核心开发语言的就有 Polkadot、Solana、Near。

需要注意的是，Rust 的语法是出了名的复杂，其学习曲线足够陡峭，其学习难度往往让人望而生畏。不过在 Rust 语言设计团队（Lang Team）在官方博客中公布的 Rust 语言 2024 年的更新路线图中，就昭示了降低学习难度是
Rust 语言的未来发展方向。 Rust 在语言设计层面比较贴近C/C++等高性能语言，所以熟悉C/C++的开发者会有稍微一点优势。

## 2. 部署和测试框架

### 2.1 概览

这部分介绍用来协助部署和测试合约代码的一些框架工具。经过此领域的不断发展，如今已经有各种各样的合约框架或工具可供使用。

### 2.2 Remix

首先是Remix，它本身不是一个框架而是一个主要基于浏览器（也支持桌面）的IDE，能够提供**基于以太坊**的在线智能合约编译、测试和部署功能，因为是基于浏览器的工具，所以不关心操作系统，直接开箱即用。
在Remix浏览器版本中编写的代码会保存在浏览器缓存中，所以不小心清除缓存就会导致你的工作区（workspace）被清空，这算是一个缺点，不过Remix后来也支持连接到电脑本地的工作区。

Remix是最早的Solidity开发工具，几乎所有的合约开发者都是从Remix开始学习。但是当开发者在合约中集成更复杂的逻辑时（较大的合约项目），就需要选择自动化程度更高的框架来开发、测试和部署合约了。

### 2.3 Truffle

Truffle是最早出现的编写以太坊合约的框架，由Consensys在2016年创建，它是基于JavaScript编写的。官方对其的介绍是：一个用来构建、测试和部署以太坊网络应用的框架。
整个框架可以当做一个套件包含三个工具：Truffle（开发和测试环境）、Ganache（通过桌面版或命令行快速部署本地EVM区块链）和Drizzle（丰富的用于构建dApp的前端UI库）。

Truffle是所有框架中历史影响最大的，你可以看到他们对行业的影响，很多框架都采用了Truffle的实践做法。你会看到大部分智能合约工程师岗位都要求掌握这个框架的使用。

### 2.4 Hardhat

Hardhat是由Nomic Labs开发的基于JavaScript的以太坊合约开发环境，能够帮助用户构建、测试和部署以太坊网络应用。Hardhat的一些重要亮点包括Solidity调试，失败交易的错误消息和显式堆栈跟踪。
内置的Hardhat网络和CLI也是Hardhat功能的重要补充。 Hardhat网络是一个专注于开发的本地以太坊网络，而CLI（命令行）则致力于与Hardhat核心功能的灵活交互。

虽然Truffle创建的较早，但后来的Hardhat正逐渐侵占Truffle的市场，因为Hardhat在测试环境、错误管理以及TypeScript集成方面拥有更好的灵活性和更小的使用成本。

下面是推荐的资源：  
[Hardhat官方入门教程_英文][2] 官方文档，持续更新  
[Hardhat官方入门教程_中文译版][3] 翻译于2020年，部分信息已经过时，但不影响入门（其中在**部署到线上网络**部分提到使用ropsten测试网，但这个测试网已经下线，需要改为其他测试网，可以查看英文版获得最新步骤）

[Hardhat使用模板][4] 官方提供，包含一个简单项目示例

### 2.5 其他框架

#### 1. Brownie

除了上面介绍的主要基于JavaScript的框架，还有基于Python的合约开发框架 [Brownie][1]，被Curve.fi、yearn.finance和Badger等项目使用，它同时支持solidity和vyper。
但这个框架的主要亮点是基于Python，Brownie的诞生是因为许多Python工程师鄙视使用JavaScript工作，并希望有一个Python的框架。
此外，大多数传统的金融技术领域都使用python而不是javascript，因此，随着Brownie的创建，从金融技术领域转移到Defi也变得更加容易。

#### 2. DappTools

这是一个是一个用Haskell构建的应用程序。不过别担心，你不需要知道Haskell就可以使用它。DappTools主要由MakerDAO团队（DAI背后的团队）使用，它的灵感来自于Unix的哲学：“一个程序只做一件事，并把它做好。
（Write programs that do one thing, and do it well.）”

DappTools是一个专注于命令行的工具，在这里，你可以使用你已经熟悉的命令行/shell工具，如bash或zsh，而不是用python、javascript或其他高级编程语言来帮助你开发。这有效地减少了一个你必须熟悉的技术，并迫使你在shell脚本方面做得更好！
它配备了一套工具，如dapp、seth、ethsign和hevm，每一个工具都是专门为智能合约开发者日常工作的必须的部分而设计的。

如果你不想学习另一种语言如 JavaScript 或 Python，希望在设置中使用尽可能少的工具，那就可以关注一下这个框架。

#### 3. Foundry

Foundry是Paradigm公司使用 Rust 对 DappTools 的一个重写版本，所以它也是一个以命令行为主的工具包。它主要包含三个组件：

- Forge：以太坊测试框架；
- Cast：用于与EVM智能合约交互、发送交易和获取链数据的一把瑞士军刀；
- Anvil：本地区块链节点，类似于Ganache，Hardhat网络。

有了Rust的加持，Foundry对合约代码的编译性能大大优于 DappTools。

## 3. 前端工具

构建dApp需要用到前端工具，除了基本的框架如React、Vue等，还有一些web3特定的三方库供我们快速使用。

### 3.1 入门

[create-eth-app][0]
是一个基于CLI快速开发以太坊应用的脚手架，它可以帮助我们通过一条命令初始化一个的目录结构清晰的项目环境，并且有多个前端框架（React/Vue）以及项目模板（default/Compound/aave/maker等）可选。
是一个非常适合新手入门使用的工具，能让我们快速了解web3 app项目开发的基本架构知识。

### 3.2 Web3.js/Ethers.js

两者都是目前流行的用以与以太坊网络交互的JS库，它们能完成的功能是差不多的，比如连接Layer1网络、查询钱包余额、监听网络变化等，对于一些更具体的介绍，推荐李留白的文章：[库对比：WEB3JS 与 ETHERSJS][8] 。

### 3.3 脚手架

[UseDapp][10] 和 [Drizzle][11] 是基于React的web3项目开发脚手架，提供了一些基础的插件和钩子，也比较常用。

### 3.4 Moralis

这个平台不仅提供了与各种区块链网络交互的不同编程语言的SDK，还同时作为一个web3基础设施存在，即提供了各种公链的Layer1网络节点服务、IPFS节点连接等等。

另外，它还提供了dApp层的API，比如NFT API、DeFi API、ENS解析API等。相对于Web3.js/Ethers.js，Moralis的功能更丰富、更全面，并且免费，推荐在项目在使用。

[Moralis EVM API][9]

## 4. 钱包

智能合约的测试、部署与线上交互都离不开钱包，钱包不仅存储我们的账户，也是一个账户与合约连接的中间工具，我们需要根据实际情况来选择使用哪个钱包。

### 4.1 小狐狸钱包（MetaMask）

它是这个领域中最广泛使用的以太坊钱包，也是一款浏览器钱包，非常方便于在浏览器中测试，是每个dApp开发者都必须掌握使用的一个钱包类型。

但是注意，小狐狸钱包是一个热钱包，它会一直与互联网连接，也就更容易受到网络攻击，攻击者可以通过网络窃取你的钱包私钥，你需要非常注意它的使用，**记得不要在小狐狸钱包上使用大额资金账户**。

### 4.2 多签钱包

小狐狸钱包属于"单签钱包"，在区块链上交易，只需要单个钱包签名即可，存在私钥泄露的**单点故障**。那多签钱包就容易理解了，它需要（多人掌握的）多个钱包提供签名才能发起一笔交易，
安全性相对单签钱包提高不少。通常在多人掌握的账户上会使用多签钱包，比如DAO或某个组织。

[多签钱包的工作原理和使用方式][12]

### 4.3 冷钱包

比如Ledger和Trezor，冷钱包的不同之处在于使用时比较**麻烦**，它通常是使用与网络隔离的某个硬件设备来保管私钥的，当需要使用钱包时，再通过USB/蓝牙等方式连接电脑使用，更常用来保管大额资金。

## 5. 区块浏览器

区块浏览器是用来浏览主网/测试网区块链账本交易详情的网站，并且支持通过地址、交易哈希和Token等属性进行搜索。除此之外，通常也提供与合约交互（若区块链支持）的功能。

- [EtherScan](https://etherscan.io/) 最流行的以太坊浏览器
- [Polygonscan](https://polygonscan.com/) Polygon链浏览器（以太坊兼容）
- [Explorer Solana](https://explorer.solana.com/) Solana链浏览器
- [TronScan](https://tronscan.org/#/) 波场浏览器
- [BscScan](https://bscscan.com/) 币安智能链浏览器（以太坊兼容）

## 6. 测试网与水龙头

几乎每个公链都有其测试网，开发者可以在其之上以几乎无成本的部署合约项目，以进行各种测试。在测试网上部署合约需要对应的原生代币，通过搜索 "**区块链名称+水龙头**"
可以找到对应区块链测试网的水龙头网站，在水龙头网站可以免费获取用于测试网的代币。

## 7. Web3基础设施
这里指的是区块链节点公共网关、去中心化存储（IPFS）等服务，在我们部署和开发时需要用到这些服务的。好在目前市场上已经有一些公司免费提供了这些服务。

- Alchemy：知名的区块链节点提供商和 API 提供商；
- Infura：提供Layer1接入、IPFS SDK使用；
- Moralis：包含上面这些服务，以及更加丰富的SDK，推荐；
- QuickNode：更丰富的区块链网络类型支持；

[0]: https://defillama.com/

[1]: https://eth-brownie.readthedocs.io/en/stable/

[2]: https://hardhat.org/tutorial

[3]: https://learnblockchain.cn/article/1356

[4]: https://github.com/NomicFoundation/hardhat-boilerplate

[5]: https://github.com/chaseSpace/learn_hardhat

[6]: https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzU5NzUwODcyMw==&action=getalbum&album_id=1716985081560367106&scene=173&from_msgid=2247500069&from_itemidx=2&count=3&nolastread=1#wechat_redirect

[7]: https://github.com/chaseSpace/learn_smartcontract

[8]: https://hicoldcat.com/posts/blockchain/comparison-of-libraries-web3js-vs-ethersjs/

[9]: https://docs.moralis.io/web3-data-api/evm

[10]: https://github.com/EthWorks/useDApp

[11]: https://trufflesuite.com/drizzle/

[12]: https://learnblockchain.cn/article/4077

### 参考

- [Top 10 Smart Contract Developer Tools You Need for 2022](https://betterprogramming.pub/top-10-smart-contract-developer-tools-you-need-for-2022-b763f5df689a)
- [对比四大智能合约语言：Solidity 、Rust 、 Vyper 和 Move](https://foresightnews.pro/article/detail/18160)
- [Hardhat Vs Truffle – Key Differences](https://101blockchains.com/hardhat-vs-truffle)