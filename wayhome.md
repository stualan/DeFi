---
timezone: Asia/Shanghai
---


---

# wayhome

1. 自我介绍

互联网老兵一枚，目前对 Defi 比较感兴趣，尤其是 Solana 和 Ton 生态，希望能借此机会了解的更深入一些

2. 你认为你会完成本次残酷学习吗？

我认为会

## Notes

<!-- Content_START -->

### 2024.08.23

- 学习 LXDAO 公开课视频 https://www.youtube.com/watch?v=_sofdktmD_8

### 2024.08.22
#### Uniswap V4 新特性

- 单例取代工厂

在 Uniswap v3 中，我们为每个流动性池部署一个新合约，这使得创建流动性池和执行多池兑换的成本更高。
在 v4 中，我们将所有流动性池保存在一个「单例」合约中，这将很大程度上节约 Gas，因为代币交易将不再需要在不同合约中持有的流动性池之间转移代币。

- 引入 Hooks

引入 hooks 在流动性池的整个生命周期中的关键点执行指定的操作——例如在交易代币之前或之后，或者在 LP 头寸更改之前或之后。

Uniswap V4 目前支持在 8 个特定的位置进行 hook 回调：

  - beforeInitialize / afterInitialize
  - beforeModifyPosition / afterModifyPosition
  - beforeSwap / afterSwap
  - beforeDonate / afterDonate

- 闪电记账系统

使用 V4 中的闪电记账系统，每个操作（交换 / 部署）只会导致内部余额更新，其中余额以「delta」为单位计价。到交换结束时，它只会在一系列计算之后换出净「delta」余额。

在 V4 中，每一个操作会更新内部的一个净余额（delta），在所有操作结束时会校验该值是否为 0，必须保证该值为 0 才能交易成功。当 Flash accounting 和 Singleton 结合时，可以大大简化多跳交易。

### 2024.08.21

#### 自动化做市商 (AMM)

常数乘积函数是自动化做市商（AMM）为资产对定价的方式。该函数构造了一个双曲线，其中对于某个常数 k，有 x = k/y。

存款人，称为流动性提供者（LPs），是这些流动性池的种子。LPs根据每个AMM的预定代币权重（在Uniswap的案例中--每个代币50%）将其代币存入流动性池。

**集中流动性**

Uniswap V3 引入了集中流动性的概念，旨在打造资本效率更高的市场。集中流动性允许流动性提供者（LPs）设定他们愿意提供流动性的价格区间，从而使资本不再均匀分散于整个恒定价格公式曲线，而是可以聚焦于市场活动更为频繁的较窄价格范围内。此外，集中流动性通过向 LPs 提供更多手续费以及增强市场深度，进一步提升了资本效率

#### **使用AMM的相关风险**

**I.价格滑点（Price Slippage）**

**II.抢跑（Front-running）**

三明治攻击

https://nigdaemon.gitbook.io/~gitbook/image?url=https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F008i3skNgy1gsat47jc8cj30x80jcq5u.jpg&width=768&dpr=2&quality=100&sign=36c2b329&sv=1

MEV 是 Maximal (or Maximum) Extractable Value 的缩写。在一个区块内，经济能量通过所有传入交易流入区块链。MEV 提取则是通过重新排序、包含和排除交易，从这些能量中收割以谋取金钱利益的行为。

搜索者通过链上数据和内存池寻找 MEV 机会

- 内存池是所有待处理交易暂存的地方，等待矿工提取并打包进下一个区块。由于该池对公众开放，搜索者会监控它以发现可能带来利润的交易
- 链上数据同样公开，亦可通过分析发现机遇。例如，搜索者可以监控以太坊在去中心化交易所（DEXs）上的价格

**III.无常损失（Impermanent Loss）**

### 2024.08.20

#### 去中心化借贷

DeFi 借贷不仅仅是通过存款赚取些许收益，更关乎实现更高程度的自我主权

DeFi 借贷在多个方面超越了传统金融借贷

- 可信中立性：用户无需前往中心化的第三方机构，即可用其资产进行借贷。智能合约全权处理包括利率、抵押和清算在内的所有事宜。
- 无许可：每个人都能平等获得贷款，任何人都可以成为出借人
- 速度：用户无需再等待贷款审批，这加快了放款流程。只要用户拥有必要的抵押物，即可借款。用户仅需准备资金和网络连接即可借款
- 透明度：由于所有交易、资金、合约及活动均在链上进行，任何人都能看到系统变动及市场状况的变化
- 可用性：应用程序可全天候从任何联网计算机访问，无需考虑银行假日，也无需员工执行交易。
- 税务影响：借贷协议允许用户在不对其抵押品产生应税事件的情况下，获得加密资产的杠杆敞口

![https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F8e574287-1db9-4703-a2c0-97eaed9de53f_606x526.png](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F8e574287-1db9-4703-a2c0-97eaed9de53f_606x526.png)

#### **APR vs APY**

- **APR（年化利率）**:
    - APR 是不考虑复利的年化利率。它表示一年中借贷的利率，但不包括因利息复投而增加的收益。
    - 公式：APR = (周期利率) × (一年中的周期数)
    
    例如，如果你每月获得 1% 的利率，那么 APR = 1% × 12 = 12%。
    
- **APY（年化收益率）**:
    - APY 则考虑了复利的影响。它表示在一年中，如果利息不断复投，最终的年化收益率是多少。
    - 公式：APY = (1 + 周期利率) ^ (一年中的周期数) - 1

         例如，假设每月的利率仍然是 1%，那么 APY = (1 + 0.01) ^ 12 - 1 ≈ 12.68%。

#### 流动性池

流动性池是由智能合约锁定的代币对或组合，例如 USDC/ETH 或 DAI/USDC/USDT/FEI。这些池为协议上发生的交易提供流动性，并使用户能够兑换进出池内特定的代币

池流动性越深，即池中每种代币数量越多，交易对池内代币相对数量及代币交易时价格变动的影响就越小。换言之，池中代币越多，每次交易产生的滑点就越少。滑点是指从一种代币兑换到另一种代币时，交易中损失的价值量

#### AMM

AMM 通过使用流动性池而非买卖双方市场来实现代币交易，是支撑去中心化交易所的核心技术

AMM 使用户能够自动且无需许可地进行交易，无需中介介入。这正是 AMMs 的真正力量所在：加密货币用户不再受制于中心化交易者和订单簿

AMM 主要有三种类型：Uniswap、Curve 和 Balancer 上的那些。Uniswap 的模式最为常见，允许用户以 50/50 的比例创建任意两种代币的流动性池。Curve 则针对相似资产创建流动性池，而 Balancer 支持最多包含八种不同代币的资产池。

#### 稳定费

稳定费是针对借出资金余额收取的可变年费率。其概念类似于信用卡的可变年利率，例如，若你借入 1,000 DAI，稳定费率为 2.5%，一年后你将欠 Maker 1,025 DAI。若在一年内还清贷款，所欠利息将按比例减少，并计算至还款交易发起的那一刻

#### 抵押率

抵押率表示为贷款所承诺抵押品价值与未偿债务价值之比的百分比

Collateralization Ratio = (Collateral Value/Debt Value) x 100

借贷协议通常会设定最低抵押率以超额抵押债务，即要求提供的抵押品价值远超所借贷款。若抵押率降至该贷款协议规定的最低要求（即清算比率）以下，贷款将被视为抵押不足，并可能被自动清算。

#### 利率模型

利率模型用于确定资产供应者因其贡献而获得的报酬，以及借款者必须为所借资产支付的金额。该模型试图平衡三个变量

- 池流动性
- 借款利率
- 供应速率

DeFi 中常见的利率模型是一种分段函数，呈现出两个不同的斜率。其设计理念在于营造一个资金池既高效利用资本，又具备足够流动性供用户进出池的环境。不同资金池针对不同的利用率目标，但总体而言，利率作为工具旨在维持目标利用率。

![https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F798dc321-0e56-46c3-ae7e-7e9865bda41b_976x436.png](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F798dc321-0e56-46c3-ae7e-7e9865bda41b_976x436.png)

在上面的例子中，该池的目标是达到 90%的利用率，这一点通过 90%处的拐点得以体现。

如果利用率较低（介于 0%至 90%之间），模型将通过低借款利率激励借贷。这些低利率会吸引用户从资金池中借取资产，从而提高利用率

然而，若利用率较高（超过 90%），借款利率会急剧上升，使得借款成本增加。此举激励借款者归还资产，以规避高利率，进而将利用率降至 90%以下。

#### **清算**

当存入的抵押品价值降至抵押率低于最低要求时，借贷平台会自动出售借款人的抵押物以偿还未结债务及可能产生的费用或罚金。债务清偿后剩余的任何抵押品将返还给借款人。

清算价格 = (未偿还债务 x (最低抵押率/100)) / 抵押代币数量

#### 闪电贷

闪电贷允许用户在极短时间内（同一区块内）无需提供抵押物即可借取资产。这类贷款通常用于不同 DeFi 协议间的套利机会。不存在资金损失的风险，因为若贷款未能在同一交易内偿还，该贷款即视为无效。

*一般来说，只要您需要一笔临时贷款且确信能在交易结束时偿还，就可以使用闪电贷*


### 2024.08.19

#### 学习稳定币相关内容

- MakerDAO
  
  MakerDAO 是一个去中心化自治组织，旨在管理以太坊上的 Maker 协议，提供稳定币 DAI 和衍生金融体系。
  RWA 作为 MakerDAO 的重要议题，被视为解决抵押品价值不稳定问题的关键方案，以支持稳定币 DAI 的大规模采用和可持续发展
  对于 MakerDAO  这样的巨型借贷协议来说，**关键的考量因素是：抵押品的价值稳定**


- RWA

  现实世界资产代币化（Real World Asset Tokenization），即将现实世界中的资产通过区块链技术进行代币化表示。现实世界资产存在于链下，所有者可从中获得预期收益，相关权属收益由法律体系规范。
  RWA 最重要的是资产端和资金端，两端都有各自的需求。

  资产端需求：

  * 现实世界资产端的需求是融资，无论是通过 Security Token Offering 的方式，还是通过抵押借贷（如 Centrifuge）的方式。
  * 资产融资的本质是获取资本的来源变为 DeFi 的即时流动性，以及利用区块链和智能合约在融资渠道上实现降本增效。
 
  资金端需求:
  * 加密资本资金端的需求是投资，关键是捕获风险低、稳定生息、可规模化、与加密波动无关的现实世界资产。
  * 从稳定的角度来看，稳定币是关键用例，作为交易媒介，不受加密波动影响；从稳定 + 生息 + 规模化的角度来看，美债 RWA 是关键用例，帮助捕获无风险收益。
  * RWA 能够创造 U 本位的生息资产，成为加密世界的一种新的资产类别，这种资产类别与 DeFi 的可组合性能够带来很大的想象空间，如生息稳定币项目和生息 Layer 2 项目。

- DAI（可简单理解成以太坊上的美元）
  DAI 是 MakerDAO 协议提供的第一个去中心化的基础稳定货币，可简单理解成以太坊上的美元

  DAI 系统运行逻辑：用户通过抵押资产创建 Vault 生成 DAI，涉及存入、借出、偿还和赎回四个操作，未偿还时会涉及利率调整和清算。
  ![DAI 原理](https://img.foresightnews.pro/202303/1261514c11f32db96f7825055e2a2f78.png)
  



<!-- Content_END -->