# mkcloud 稳定性：真实延迟数据、维护记录与全部套餐价格一次看懂

搜"mkcloud 稳定性"的人，基本都卡在同一个疑问上：这家 2023 年上线的国人专线商家，宣传页写着"物理服务器资源独享、全天候监控、系统高可靠无抖动"，价格却只有大厂国内 BGP 流量费的零头，把正经业务放上去到底稳不稳？这篇文章把官方购物车的现行价格、第三方实测数据和官方通知里的维护记录摊开说，帮你判断它值不值得买、适合买哪条线。

## 先给结论：mkcloud 的稳定性处于什么水平

先把四条主力线路的端内延迟放在一张表里，这些数字来自当前官方购物车的标称口径，早期第三方实测与之基本一致：

| 线路 | 国内入口 | 出口 | 端内延迟 | 主要用途 |
| --- | --- | --- | --- | --- |
| 广港 IEPL | 腾讯广州八线 BGP | 香港 BGP | 1~2ms（早期实测约 3ms） | 华南办公、对港业务、TikTok 直播 |
| 沪港 IPLC | 上海电信 | 香港 BGP | 21ms | 上海方向日常对港 |
| 沪日 IPLC | 上海电信 | 日本 BGP | 25~28ms | 对日电商、游戏出海 |
| 沪美 IPLC | 上海电信 | 美国 BGP | 124~134ms | 美区业务、独立站 |

端内延迟只是下半段。用户真正关心的是晚高峰的表现，这方面一份 2026 年的第三方测评给出的数据是：正常时段基本 0 丢包，晚高峰丢包率控制在 1% 以内，并且认为其稳定性好于不少普通 CN2 GIA 线路。2023 年 Record LOGS 的早期测评则提到，广港入口为 UCloud 广州八线 BGP，"国内互联及其优异，全国各大运营商的 ping 值都很不错"，端内 ping 稳定在 3ms 左右。

还有一点对"稳定性"很关键：每台专线 VPS 都配 **2 个独享 IPv4（一进一出）**，不是共享池轮换 IP。早期测评用多家数据库测过出口 IP，scamalytics 欺诈评分 0/100， abuse 得分 0。对跨境店铺和广告账户来说，固定且干净的 IP 本身就是稳定性的重要组成部分。

但要把丑话说在前面：mkcloud **默认不提供 SLA**，官方知识库明确写了"没有默认赔付或可用性指标保证"，需要保障得单独询价定制。也就是说，它的稳定靠的是线路质量和资源独享，而不是合同承诺。下面几节会把这个判断拆开讲。

判断归判断，价格和档位随时会调整，建议下单前自己核一遍：👉 [查看全部线路的当前价格与档位](https://bit.ly/MKCLoud)

## 稳定性背后的三个设计：白名单、独享资源与诚实的带宽标注

mkcloud 的稳定表现，有几条官方规则在支撑，同时也有几条限制直接影响你的使用体验。

**第一，省级 IP 白名单。** 所有专线产品（高防款除外）只允许一个省份的 IP 连入，开通时选省份，后续可以改。官方的解释是防止机场和转发滥用——共享带宽没了"万人骑"的损耗，晚高峰表现才有保障。副作用是你要是经常跨省出差，得记得先改白名单，或者走拉新活动攒城市群白名单。

**第二，物理资源独享加全天候监控。** 这是官网对"持久稳定"的官方口径。从第三方跑分看，机器本身不拖后腿：AMD EPYC 平台、KVM 虚拟化、磁盘 4K 读写 65MB/s 以上，属于正常 VPS 水平，重点资源确实花在线路上。

**第三，官方对带宽的描述相当诚实，甚至偏保守。** 知识库原话：共享带宽是峰值，不保证持续跑满；独享款不限流量，但也不保证 24 小时对任意目标满速。计量型套餐按上行加下行**双向**统计流量，用完就停，可以自助购买流量重置或者提交工单补差价升级。早期测评折算过，广港单向流量成本约每 GB 0.7~0.8 元，与国内 BGP 的行情基本对齐。换句话说，你买的钱大部分花在跨境路径上，而不是机器配置上。

实际吞吐还会受协议、对端服务器和你本地网络影响。官方知识库甚至专门提醒：不能把店铺封停、转化率波动直接归因于线路。这种不给自己贴金的写法，在商家里不多见。

## 维护、故障与补偿：这家商家出过哪些状况

判断长期稳定性，光看测速没用，得看它出事之后怎么处理。mkcloud 有官方 Telegram 通知群，维护和故障都会提前或事后公示，翻一下历史记录，能看到这些信息：

- **例行维护**：比如 2025 年 2 月广港专线因机器配置升级，凌晨 7:00~7:20 维护，约 20 分钟停机。选在低峰期、提前通知、控制在半小时内，属于行业常规操作。
- **故障补偿**：出现过故障时，官方给全部客户、全部产品统一延长 1 天到期时间。
- **迁移专项补偿**：香港专线机房迁移期间因频繁维护影响体验，官方对所有香港专线产品补偿：到期时间统一延长 1 天，迁移前消耗的流量全部免费重置。
- **风险提示**：通知群里对"先锋版"这类产品明确标注"可能会有部分不稳定现象，购买即代表已了解并同意承担相应风险"。把不稳定预期写在购买前，至少态度是坦率的。

第三方测评对售后还有一条实用经验：高峰期在线客服基本联系不上，遇到问题直接提工单，技术团队一般 12~24 小时内能解决。

还有个时间维度的参考：2023 年底 rclogs 测评时的结论是"新商家，只建议月付"。到现在官网页脚标着 2026 年版权、知识库和商店持续更新，这家商家已经稳稳运营了约三年，早期"担心跑路"的问题至少被时间部分消化了。月付依然是试水首选，这个建议没变。

## IX 上云互联：便宜档位的稳定性前提

mkcloud 全场最便宜的一档，2TB 流量、1G 峰值带宽，月付 158 元，属于 IX 上云互联产品线。它稳定性没问题，但有一条很多人忽略的前提：**它不是从你家宽直接连入，而是要一台云厂服务器当前置**。

IX 款的入口是"云厂 BGP 优化网络通道"，只允许云厂 BGP 网络连入，需要你先有一台阿里云、腾讯云、百度云之类的国内云服务器，把业务跑在云上，再经优化通道走专线出去。而且要留意两地的支持范围并不相同：

- 广东-香港 IX：支持腾讯云国内全网、百度云国内全网、火山云华南、华为云华南，**阿里云国内全网暂时不通**；
- 上海-香港 IX 和上海-日本 IX：支持阿里云国内全网、腾讯云国内全网、百度云国内全网、火山云华东、华为云华东、UCloud 华东。

官方知识库也提醒得很直白：IX 款要比较的是"本地到前置云、再到 IX VPS"的完整链路体验，不能只看跨境端内的 1~2ms。另外 IX 款大多标注"超量停机"，个别新品是预售制、无法立刻开通。如果你的业务本来就跑在云上，IX 是性价比最高的选择；如果你的业务在本地宽带上，直接看下面的共享专线款更省心。先确认自己的云厂在不在支持列表：👉 [确认你的云厂能否直连 IX 线路](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh)

## 全部套餐与当前价格（2026 年 9 月官网购物车实抓）

以下三张表覆盖官网当前展示的全部产品线与档位，价格均为人民币月付，均为"入口 IP + 出口 IP"双独享 IPv4 配置。流量计费款按上下行双向统计。

**表一：四大主流共享带宽专线（流量计费）**

| 线路 | 配置 | 峰值带宽 | 月流量 | 月付 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 广港 IEPL | 1核2G/20GB | 200M | 1TB | ¥358 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 广港 IEPL | 2核4G/40GB | 300M | 2TB | ¥568 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 广港 IEPL | 2核4G/40GB | 300M | 4TB | ¥998 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 广港 IEPL | 4核8G/60GB | 500M | 6TB | ¥1388 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 广港 IEPL | 4核8G/60GB | 500M | 10TB | ¥2288 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 广港 IEPL | 4核8G/60GB | 1G | 20TB | ¥4500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-sh) |
| 沪日 IPLC | 1核2G/20GB | 200M | 1TB | ¥358 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪日 IPLC | 2核4G/40GB | 300M | 2TB | ¥568 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪日 IPLC | 2核4G/40GB | 300M | 4TB | ¥998 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪日 IPLC | 4核8G/60GB | 500M | 6TB | ¥1388 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪日 IPLC | 4核8G/60GB | 500M | 10TB | ¥2288 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪日 IPLC | 4核8G/60GB | 1G | 20TB | ¥4500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-jp-sh) |
| 沪港 IPLC | 1核2G/20GB | 200M | 1TB | ¥288 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪港 IPLC | 2核4G/40GB | 300M | 2TB | ¥428 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪港 IPLC | 2核4G/40GB | 300M | 4TB | ¥696 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪港 IPLC | 4核8G/60GB | 500M | 6TB | ¥988 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪港 IPLC | 4核8G/60GB | 500M | 10TB | ¥1536 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪港 IPLC | 4核8G/60GB | 1G | 20TB | ¥3072 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-sh) |
| 沪美 IPLC | 1核2G/20GB | 200M | 1TB | ¥428 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |
| 沪美 IPLC | 2核4G/40GB | 300M | 2TB | ¥698 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |
| 沪美 IPLC | 2核4G/40GB | 300M | 4TB | ¥1258 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |
| 沪美 IPLC | 4核8G/60GB | 500M | 6TB | ¥1758 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |
| 沪美 IPLC | 4核8G/60GB | 500M | 10TB | ¥2888 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |
| 沪美 IPLC | 4核8G/60GB | 1G | 20TB | ¥5666 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-us-sh) |

**表二：IX 上云互联专线（需云厂前置，超量停机）**

| 线路 | 配置 | 峰值带宽 | 月流量 | 月付 | 购买 |
| --- | --- | --- | --- | --- | --- |
| 广东-香港 IX | 2核4G/40GB | 1G | 2TB | ¥158 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 2核4G/40GB | 1G | 4TB | ¥258 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 4核8G/40GB | 2G | 6TB | ¥378 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 4核8G/40GB | 2G | 10TB | ¥826 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 4核8G/40GB | 2G | 20TB | ¥1639 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 4核8G/60GB | 3G | 30TB | ¥2458 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 8核8G/60GB | 3G | 50TB | ¥3588 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 8核16G/80GB | 5G | 100TB | ¥7168 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 8核16G/80GB | 5G | 200TB | ¥12288 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 广东-香港 IX | 8核16G/80GB | 5G | 300TB | ¥18428 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-hk-sh) |
| 上海-香港 IX | 2核4G/40GB | 500M | 2TB | ¥198 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 2核4G/40GB | 500M | 3TB | ¥288 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 4核8G/40GB | 1G | 6TB | ¥398 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 4核8G/40GB | 1G | 10TB | ¥666 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 4核8G/40GB | 1G | 20TB | ¥1290 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 4核8G/60GB | 2G | 30TB | ¥1900 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-香港 IX | 8核8G/60GB | 2G | 50TB | ¥3120 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-sh-hk-sh) |
| 上海-日本 IX | 2核4G/40GB | 200M | 1TB | ¥166 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 2核4G/40GB | 300M | 2TB | ¥268 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 2核4G/40GB | 500M | 3TB | ¥358 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 4核8G/40GB | 1G | 6TB | ¥688 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 4核8G/40GB | 1G | 10TB | ¥1125 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 4核8G/40GB | 1G | 20TB | ¥2150 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 4核8G/60GB | 2G | 30TB | ¥3165 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |
| 上海-日本 IX | 8核8G/60GB | 2G | 50TB | ¥5222 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=cloud-jp-sh) |

**表三：独享带宽、高防与 CN2 产品（流量不限）**

| 产品 | 配置 | 独享带宽 | 月付 | 购买 |
| --- | --- | --- | --- | --- |
| 广港 IEPL 独享 | 2核4G/40GB | 5M | ¥500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 2核4G/40GB | 10M | ¥700 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 2核4G/40GB | 20M | ¥1320 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 4核8G/60GB | 50M | ¥3150 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 4核8G/60GB | 100M | ¥5800 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 4核8G/60GB | 200M | ¥11600 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 广港 IEPL 独享 | 4核8G/60GB | 300M | ¥17400 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex) |
| 沪港 IPLC 独享 | 2核4G/40GB | 5M | ¥650 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-ex) |
| 沪港 IPLC 独享 | 2核4G/40GB | 10M | ¥950 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-ex) |
| 沪港 IPLC 独享 | 2核4G/40GB | 20M | ¥1760 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-ex) |
| 沪港 IPLC 独享 | 4核8G/60GB | 50M | ¥4000 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-ex) |
| 沪港 IPLC 独享 | 4核8G/60GB | 100M | ¥7500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-hk-ex) |
| 厦港高防 IPLC | 4核8G/40GB | 200M | ¥6000 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex) |
| 厦港高防 IPLC | 8核8G/60GB | 500M | ¥13500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex) |
| 厦港高防 IPLC | 28核64G/512GB | 1G（赠独立服务器） | ¥24000 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex) |
| 厦港高防 IPLC | 28核64G/512GB | 2G（赠独立服务器） | ¥46000 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex) |
| 厦港高防 IPLC | 28核64G/512GB | 5G（赠独立服务器） | ¥110000 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex) |
| 上海 CN2 | 8核16G/60GB | 500M（送上海9929出口，7天交付） | ¥4500 | [ 选购](https://www.mkcloud.net/aff.php?aff=390&pid=sh-cn2-ex) |

几点补充说明，都是影响下单决定的信息：

- **计费周期**：购物车支持月付、季付、半年付、年付乃至三年付。以官方知识库确认的沪港入门款为例，季付 864 元、年付 3456 元，正好等于月付乘以月数，官方没有承诺年付折扣，别按"年付自动便宜"做预算。
- **优惠码现状**：官方知识库里保留的 MK-8.8（流量款 8.8 折循环）、MK-7.8（独享首月 7.8 折）、MK-IEPL-WELCOME（IEPL 9 折）等均标注为历史活动码、活动期有效；2026 年仍有第三方优惠码汇总站和测评称部分码可循环使用。最可靠的办法是下单时在优惠码框里试一下，能不能折以购物车实算为准。
- **入口变体**：广港独享另有广东移动、广东电信、广东联通及广东三线入口版本，沪港独享为 UCloud 上海 BGP 入口，高防系列还有泉州电信入口的泉港款，均可在对应线路页切换网络后选择。独享带宽档位如果表格里没有你要的规格，最大一档是"自定义"，实际按需求询价：👉 [查看独享带宽的可选档位](https://www.mkcloud.net/aff.php?aff=390&pid=gz-hk-ex)
- **在售变化**：早期测评里的广港 500GB 档（198 元/月）等配置已不在当前在售列表，目前广港共享起步就是 1TB 档 358 元，别按旧文章的价格做预算。

需要长时间满速跑传输、或者业务容易被打的，重点看表三的独享和高防线，官方对高防款的说明是默认含 100Gbps 高防、防御可定制升级、可申请开通无视海外攻击与 UDP 攻击，而且这条线没有省份白名单限制：👉 [查看厦港高防专线的完整配置](https://www.mkcloud.net/aff.php?aff=390&pid=xm-hk-ex)

## 退款、实名与合规：买之前必须知道的几条

稳定性之外，这几条规则直接决定 mkcloud 适不适合你。

**实名是硬门槛。** 所有产品需中国身份信息实名，国内手机号、身份证号、姓名一致性验证，缺一不可。没有国内身份信息的用户直接排除。

**退款只认质量问题。** 官方口径：仅质量问题支持退款，需要在工单中提交测试截图和具体数据（准确的延迟、速度），由官方审核判断，不支持"不想要了就退"，而且**服务开通后不支持更换到其他地域**。选线路之前想清楚方向，选错了没有反悔药。第三方测评提到开通后 24 小时内集中测试、有问题尽快提工单，算是个可操作的加分项，具体以官方服务条款为准。

**用途红线要背熟。** 禁止机场、翻墙回国等违规用途，违者清退不退款。所有专线采用省级白名单就是为这个设计的。正经做跨境电商、企业组网、对外部署服务的用户不受影响，想拿来当共享节点用的，这家不适合你。

**没有 SLA。** 前面提过，默认没有可用性承诺和赔付条款，对稳定性有合同级要求的，先提交工单询价定制。

## 哪些人适合，哪些人绕行

基于以上全部核验信息，mkcloud 适合这几类用户：业务跑在阿里云、腾讯云等国内云上，想要 158 元起低成本出海的团队（IX 款）；对延迟极度敏感、需要干净固定 IP 的跨境卖家和 TikTok 运营者（广港 IEPL，端内 1~2ms）；从上海方向对港、对日有持续业务的企业（沪港、沪日 IPLC）；以及有持续大带宽或高防需求的进阶用户（独享与厦港高防款）。

不适合的也很明确：预算几十块的个人翻墙需求（这是合规专线 VPS，不是机场）；没有中国身份信息无法实名的用户；需要 SLA 合同保障的关键业务；以及想开通后随便换地域的用户。

最后给个务实的操作路径：先用 IX 或广港共享的最低档月付认真测一周，把晚高峰延迟、丢包和你业务接口的实测数据记下来，合适再上长周期，不合适，质量问题工单里附上数据也说得清楚。选好方向就可以动手了：👉 [去 Mkcloud 选一条适合你业务方向的线路](https://bit.ly/MKCLoud)
