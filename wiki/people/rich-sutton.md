# Rich Sutton（Oak Lab 联合创始人，强化学习奠基人之一）

来源：[Training Data / Sutton & Javed](../videos/20260818-training-data-sutton-javed-continual-learning-oak.md)（本页时间戳均出自该期，也是本库目前收录他本人的唯一一期）

- **背景**：主持人介绍他开创了强化学习、写了该领域的经典教科书，Dave Silver 是他的学生，并写了《The Bitter Lesson》（2019）（[00:01:01]）。2003 年加入 University of Alberta（[00:02:01]–[00:03:01]）；2022 年提出 12 步的 Alberta Plan for AI research（[00:36:16]）。
- **现任**：与学生 [Khurram Javed](khurram-javed.md) 联合创办 Oak Lab，目标是让 agent 持续从自身经验中学习。
- **阅读边界**：以下是他作为 Oak 创始人的观点。他对 Oak 路线和时间表的判断没有在本期给出实验数据。

## 主要观点

- **持续学习就是学习**：他认为学习本来就该是持续的，需要 continual learning 这个词说明领域走偏了（[00:04:02]–[00:05:02]）。
- **Bitter Lesson 的本意**：不要依赖人类知识，专注能随算力扩展的方法，如搜索和学习；需要的是能随算力扩展的好算法，而不是不要算法（[00:08:03]–[00:09:03]）。他强调先验知识和学习原则上不冲突，应该是"朋友"（[00:18:07]–[00:19:08]）。
- **LLM 的定位**：既是 Bitter Lesson 的正例，也是反例，最终受限于有限的互联网数据（[00:09:03]–[00:10:04]）；部署后"权重从不改变"，所以不算在学习（[00:22:09]）。他同时称 LLM 是意料之外的重大科学突破，但只占智能的约 20% 到四分之一（[00:49:25]–[00:50:26]）。
- **合成数据**：称其为"一个大错误"，因为生成数据的程序只是一个小世界（[00:11:04]、[00:14:04]）。
- **监督学习不是动物学习的方式**：没人能告诉我们肌肉该怎么动，学校只占学习的一小部分（[00:26:11]–[00:28:13]）。人与动物只是程度差别（[00:31:14]）。
- **领域最缺的能力**：学出世界模型、再用它规划。棋类和数学之所以能规划，是因为规则已知（[00:35:16]）。
- **灾难性遗忘可以治**：每个权重元学习自己的步长，加上在 feature 空间做 generate and test；具体算法是他们发表在 Nature 上的 continual backprop（[00:39:18]–[00:41:19]）。
- **Oak 最大的野心**：一个能持续训练自己、同时保持自洽的心智，覆盖从细小动作到大尺度计划的知识（[00:43:21]–[00:45:22]）。未来会是"单一设计、很多个心智"（[00:50:26]）。

## 本库其他提到他的地方

- [谢赛宁](xie-saining.md)借 Dyna 讲模型与规划，并转述过他关于松鼠的说法（[视频页](../videos/20260316-zhang-xiaojun-xie-saining-world-models.md)）。
- [刘子鸣](liu-ziming.md)用 Bitter Lesson 论证长期不需要人为结构（[视频页](../videos/20260731-zhang-xiaojun-liu-ziming-ai-for-ai.md) [00:57:07]）。
- [Pushmeet Kohli](pushmeet-kohli.md)回忆在 DeepMind 时听他讲 bitter lesson（[视频页](../videos/20261010-latent-space-alphafold-didnt-solve-protein-folding.md) [00:05:04]）。
- [Jason Ma](jason-ma.md) 的 Dyna Robotics 公司名取自他的 Dyna 论文。
