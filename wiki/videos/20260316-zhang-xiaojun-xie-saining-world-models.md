# 谢赛宁：从表征学习到预测大脑，为什么与杨立昆创立 AMI（张小珺 #133，2026-03-16）

- **嘉宾**：[谢赛宁（Saining Xie）](../people/xie-saining.md)，采访时任纽约大学教师、AMI Labs 联合创始人兼首席科学官；身份来自本期介绍。
- **主持**：[张小珺](../people/zhang-xiaojun.md)。微信对话逐段具名，发言归属以该编辑版为依据，不根据匿名声音猜人。
- **完整节目入口**：[YouTube](https://www.youtube.com/watch?v=iiBY0fqpThI) · [小宇宙](https://www.xiaoyuzhoufm.com/episode/69b77577f8b8079bfa8eb837)，约 405 分钟。节目发布于 2026-03-16，采访据作者介绍录于 2026-02。
- **本页实际信源**：[微信原文](https://mp.weixin.qq.com/s/PIOh_aXVuNUT27G5UoKCkw) · [归档文字与段落定位](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md) · [用户提供的原始 HTML](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/wechat-original.html)。原文作者张小珺，微信显示发布时间为 2026-03-16。

> **覆盖范围：微信公众号编辑节选的完整整理，不是七小时完整版的完整总结。** 2026-11-09 摄取时 YouTube 没有可下载字幕。微信作者明确说明为优化后的节选，并省略学术生涯、JEPA、Research taste 等大段内容。本页引用 P 编号指向归档段落，不是音视频时间。未经逐段核对的节目章节时间仅放在末尾导航。原文的人物回忆、融资数字、技术评价及预测，分别保留其叙述身份，不作为独立核实结果。

另存有[微信正文完整文本提取](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/wechat-fulltext.txt)，包含 HTML 正文中的非段落元素；P 编号版用于定位，原始 HTML 与完整文本用于核对排版中标题、提问等内容。

## 先读这五条

1. **世界模型预测动作造成的状态变化。** 谢赛宁纠正了主持人的理解：不是直接预测下一个动作，而是给定状态与动作，预测后续状态，再服务规划与决策。（[原文 P135–P157](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p135)）
2. **表征要保留决策需要的信息。** 他希望学习层次化的潜在状态，不追求把世界的所有纹理和物理细节重建一遍。（[原文 P157–P165](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p157)）
3. **他批评语言捷径，同时承认 LLM 的贡献。** 语言可能让多模态任务靠统计线索过关，但他明确说 LLM 是智能体的重要部分，也不把世界模型与 LLM 简单视为替代关系。（[原文 P192–P219](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p192)）
4. **AMI 的组织与数据策略是一体的。** 他设想与有真实任务和数据的产业伙伴合作，形成模型、应用价值和新增数据的循环；这仍以研究突破能够发生为前提。（[原文 P030–P049](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p030)、[P105–P119](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p105)）
5. **关键训练问题没有解决。** 他把输入指向连续、高维、有噪声的真实信号，但明确承认最优输出目标函数仍是研究问题。这是理解整期技术雄心必须同时保留的限定。（[原文 P369–P372](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p369)）

## 一、世界模型、表征与规划

谢赛宁给出的是一个状态转移框架，可概括为 `s_next = f(s, a)`：给定系统状态和动作或干预，预测后续状态。他提醒世界模型不必限于时间预测；这个公式只是访谈中最基本的例子。这里的动作是预测函数的条件，不能把世界模型直接等同于输出动作的 policy。（[原文 P135–P157](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p135)）

他用 MPC 说明模型怎样用于决策：采样候选动作序列，通过模型 rollout，计算与目标的代价，执行较好序列的第一步，再根据新状态重复。他还借 Sutton 的 Dyna 解释模型、规划和学习之间的联系。这些是他对既有控制与强化学习思想的讲解，不能算作 AMI 已实现的新能力。（[原文 P140–P153](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p140)）

在他看来，核心难题是状态怎样表示：若目标是聊天，不必保留桌面每一点纹理；若要建模飞机，也不会逐个模拟分子。表征学习要把原始数据映射到对下游任务有用的空间，逐层形成更抽象的状态，而不是无限增加可见细节。（[原文 P157–P165](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p157)、[P185–P188](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p185)）

**本库的区分**：预测准确性、状态充分性与闭环控制可靠性是三项需要分别检验的要求。访谈提出了方向和类比，没有给出能够把三者同时验证的 AMI 实验结果。

## 二、为什么批评 LLM，也不否定 LLM

### 语言提供了方便的接口，也可能遮蔽视觉能力缺口

谢赛宁承认语言让视觉从固定分类、检测等任务拓展到更自由的多模态交互；他的担心是，一些任务可以主要依赖语言统计而不真正利用视觉。所谓语言对视觉的「污染」，在此首先是对学习捷径和评价方式的批评，不是证明语言输入必然损害所有视觉模型。（[原文 P271–P312](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p271)）

他把语言称为带有人类文明预处理的监督信号，因而主张从更广的来源看，语言建模有很强的监督成分。这是他对数据来源的解释；不能把它直接改写为标准机器学习术语中 next-token prediction 不属于自监督学习。（[原文 P297–P304](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p297)）

### Bitter Lesson 与 Scaling Law 的争论

他认为语言已经封装了人类知识与抽象，过度依赖它不符合其理解的 Bitter Lesson；甚至像素格子也不是最终形式。他希望模型学到可供系统自身使用的潜在表征，渲染给人看的结果只是接口。他同时承认语言未来仍会占重要位置。（[原文 P168–P176](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p168)、[P216–P219](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p216)）

他认为语言模型的规模收益混合了事实知识检索与世界理解，因此不能由榜单提升直接推断后者；他预期世界模型的 scaling 行为不同，但未给出已验证的通用定律、参数或数据配比。（[原文 P190–P195](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p190)、[P297–P302](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p297)）

**技术表述边界**：原文称 Transformer 对每个 token 赋予相等注意力，不能作为注意力权重必然相等的事实；这里保留的是他对逐帧 token 化造成冗余和效率问题的批评。原文把压缩称作「无损压缩」，也没有给出严格的信息论定义，本页不据此建立定量推论。（[原文 P190–P199](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p190)）

### 安全能力是主张，不是保证

他认为学会预测动作后果，可以在推理阶段避开危险动作，并批评仅靠微调和 RL 约束行为的方式。他用持刀机器人的例子解释这一点。**本库限定**：错误的世界模型、遗漏的危险因素或不合适的代价函数仍可能导致危险；有预测能力不等于已经解决安全与对齐。（[原文 P178–P182](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p178)）

## 三、数据、产品出口与不同世界模型路线

谢赛宁希望由互联网视频起步，再取得不上传到互联网的工业和真实生活数据；输入最终应超出视觉，包括连续、高维、可能有噪声的传感信号。「下载人类」是其数据方向的比喻，访谈未给出完整采集、权限、成本和训练方案。儿童视频与语言 token 的量级对比也未统一计量单位，不作定量结论。（[原文 P105–P110](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p105)、[P221–P223](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p221)）

他点名两类应用：always-on 智能眼镜或个人助理，以及机器人。他想通过预训练和「大脑」研究帮助机器人，而不必一开始自己造本体；同时承认真机验证很重要。这是应用设想和分工选择，非产品已交付。（[原文 P224–P232](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p224)、[P290–P295](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p290)）

他把视频生成公司偏重的 world simulator、World Labs 偏重的显式空间表征，以及 AMI 设想的 predictive brain 区分开。主持人追问是否认为 World Labs 无法提升智能时，他明确承认对方也可能通过训练智能体提升智能，并称两条路线互补。**这是谢赛宁对同行的分类，不能取代同行自己对路线的说明**；其中「保证 100% 不出错」之类措辞不作为可靠性结论。（[原文 P315–P321](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p315)）

## 四、AMI：重新定义问题的组织实验

谢赛宁用「叙事 → benchmark → 资源分配」解释为什么研究员即便认为视频理解重要，也会被配置去服务视频生成的标注工作。他担心研究竞争逐渐变成固定目标下的资源竞争，压缩重新定义问题的空间。这是他对行业环境的判断，不是对所有实验室的调查结论。（[原文 P079–P090](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p079)）

他回忆与 LeCun 对创业方向迅速达成一致，自己定位于科学工作，公司由 Alex LeBrun 任 CEO。他设想由产业伙伴共同提供问题、数据及验证，形成研究和应用闭环；他明确说 AMI 不是纯学术实验室，也不会把全部研发开源。（[原文 P030–P049](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p030)、[P060–P069](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p060)、[P116–P121](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p116)）

关于四个中心和不选硅谷，他把巴黎、纽约、蒙特利尔、新加坡与全球伙伴网络联系起来，并批评硅谷对 LLM 的共识过强；他也不排除以后去硅谷。不能把标题「逃出硅谷」理解为永久退出美国或全面否定硅谷。（[原文 P035–P052](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p035)）

他希望降低研究员的过强 ego，同时保留年轻人的可见度和成长空间；他不相信只把成名的「超级英雄」聚在一起就会自然产生突破。他承认自己没有创业成败经验，并把研究突破作为整个商业设想成立的前提。（[原文 P097–P099](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p097)、[P113–P119](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p113)）

原文导语称 AMI 当时约 25 人、融资 10.3 亿美元、投前估值 35 亿美元；这些是作者在 2026-03 的介绍口径，不是截至本页整理日期的公司现状，也未在本任务中独立核实。（[原文 P002–P003](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p002)）

## 五、人物经历、智能观与价值选择

他回忆 2018 年获得 OpenAI offer 后选择 FAIR，主要因为希望与何恺明、Piotr Dollár、Ross Girshick 一起做视觉研究；2024 年又在刚开始 NYU 工作时拒绝 Ilya 的 SSI 邀请。关于 Ilya 的语气、对感知模型的判断和讨论「爱」的内容，都是谢赛宁单方回忆。他自己不把路线差异归结为必须你死我活的分歧。（[原文 P235–P267](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p235)）

他反对用人类擅长的高阶符号任务概括全部智能，强调动物的感知、行动和生存能力。他仍以有益于人的类人智能为目标，但主张先检验机器人在真实生活中的可靠性。他转述 Sutton 关于松鼠智能的观点，不能把转述直接当成 Sutton 本人的已核实原话。（[原文 P346–P372](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p346)）

他用 Klopp 的 normal one 与「电池」比喻自己希望承担的团队角色：给团队持续提供能量；他谈到研究中迷茫和沮丧的常态，也强调走出技术圈的回音壁。他以人与人的真诚交流作为更底层的价值，认为学术作品本身也能建立信任。（[原文 P380–P419](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p380)、[P438–P446](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p438)）

他推荐《集异璧之大成》与《禅与摩托车维修艺术》，也谈及《疑犯追踪》（POI）、《万神殿》等作品。结尾「42」是计算资源与科幻典故的对话，不是给智能、命运或物理世界建立了可计算的统一理论。（[原文 P420–P458](../../sources/zhang-xiaojun/20260316-iiBY0fqpThI/transcript.md#p420)）

## 六、与本库已有材料怎么并读

- [李飞飞 / World Labs](../people/fei-fei-li.md)：并读空间智能与表征接口。本期对同行路线的描述来自谢赛宁，宜与李飞飞自己的访谈分开理解。
- [Jason Ma / Dyna](../people/jason-ma.md)：并读世界模型、预训练数据和工作流自主性。两者都关注物理任务，但研究目标、数据来源和部署验证并不相同。
- [姚顺宇](../people/yao-shunyu.md)：并读语言、Agent 与环境交互。比较时应检查讨论的是数字环境任务还是连续物理环境，不能把任务差异都视为路线冲突。
- 相关主题：[物理 AI 与机器人](../topics/physical-ai-and-robotics.md)、[训练管线](../topics/llm-training-pipeline.md)、[实验室文化](../topics/ai-lab-culture.md)、[评估与 Benchmark](../topics/evaluation-and-benchmarks.md)、[LLM 安全](../topics/llm-security.md)。

## 七、完整版回听导航与未覆盖内容

以下为小宇宙节目介绍给出的章节起点的近似分钟导航，**只针对音频版，未证明与 YouTube 时间轴逐秒一致，也不是本库转录稿锚点**。这些分钟数不用于给本页观点作时间戳背书。

| 原节目章节 | 音频版章节起点 |
|---|---|
| The normal one | 开始后约 1 分钟 |
| 世界总不让我做 Vision | 约 36 分钟 |
| 学术流浪；与何恺明的友谊 | 约 52 分钟；约 58 分钟 |
| 两次拒绝 Ilya | 约 81 分钟 |
| 杨立昆和李飞飞往事 | 约 98 分钟 |
| 表征的世界 | 约 118 分钟 |
| Research taste 与《金刚经》 | 约 164 分钟 |
| 世界模型是什么 | 约 251 分钟 |
| 从下载互联网到下载人类 | 约 270 分钟 |
| AMI 创立过程 | 约 298 分钟 |
| 硅谷被催眠了 | 约 346 分钟 |
| 自大的人类；42 | 约 367 分钟；约 379 分钟 |

微信明确省略的完整论述包括：学术流浪和导师关系、Cambrian-S 的电影启发、JEPA 路线演变、Research taste 与《金刚经》、对 Impact 一词的看法及维特根斯坦讨论。**这些不能视为本页已总结内容**，须取得全文字幕或完成音频转录后增量补齐；本页与已有原始文件保留，新增信源单独归档。
