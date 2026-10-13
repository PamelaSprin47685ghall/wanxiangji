[GUIDE: Apply ASD-STE100 to source code, Mise-en-place to code design and thinking framework. Adapt Gall’s Law, Chesterton’s Fence, and Poka-yoke. Invoke Goodhart’s Law and Via Negativa when needed. Treat these principles as Wittgenstein’s Ladder. Build the real thing, not its imitation. Try to falsify it.] [For natural-language discussion, follow Fei Xiaotong’s plain precision and Kunihiko Kodaira’s quiet clarity. Avoid officialese, performative rhetoric, translationese, and textbook cadence. Let the subject shape the prose.]

# AXIOM
1. [开发者] AXIOM 必须直接对应使用者或开发者真正在乎的事，并标注理由。
    - 理由：不写理由，规则就无从验证，也判断不了该删还是该留。
2. [开发者] LEMMA 必须是 AXIOM 或其他 LEMMA 的推论，并标注推理过程。
    - 理由：推理写明白，结论才能被复核、被推翻。
3. [开发者] SPEC 必须是 LEMMA，且能被生产或测试代码证明成立，并标注证明。
    - 理由：代码证明不了的规范落不了地。
4. [开发者] 所有代码和文档都是以上三者的衍生品，而且在满足它们的前提下最简实现。
    - 理由：需求要有出处，实现要能删、能改。
5. [使用者] 如果软件不能让用户满意，则需要进一步演绎出更多 LEMMA/SPEC。
    - 理由：用户满意与否是最终的验收标准。
6. [开发者] 如果演绎出更多 LEMMA/SPEC 的过程中发现无法判定句，考虑归纳分析出新的 AXIOM。
    - 理由：不补公理，演绎就卡在无法判定的地方。
7. [开发者] 在前六条可满足时，AXIOM、LEMMA、SPEC 三者的复杂程度越低越好，称之为奥卡姆剃刀。
    - 理由：体系越简单，越看得懂，越守得住。
8. [开发者] 避免编译很慢，避免耦合和复杂程度飙升。
    - 理由：编译慢拖垮反馈速度，耦合和复杂程度拖垮修改。

# LEMMA
1. [AXIOM: 1, 2, 3, 6, 7] 接手项目时，有时 SPEC 其实应该重命名为 LEMMA 或上溯到 AXIOM：从实现细节反推原始需求，称之为第一性原理。
    - 推理：AXIOM 1–3 给出各层判定标准，旧条目据此可重判；AXIOM 6 遇无法判定句本就要求上溯；AXIOM 7 要求体系最简，重整常优于新增。
2. [AXIOM: 7] 有时可以把 AXIOM/LEMMA/SPEC 的集合重组，就像数学上的公理系统变换，目的是简化理论。
    - 推理：AXIOM 7 要求复杂程度最低，公理系统变换正是达到最简的手段。
3. [AXIOM: 4, 5] 很多代码是可以删除的。如果发现事实上不能删除，要形式化成 AXIOM/LEMMA/SPEC。
    - 推理：AXIOM 4 要求最简实现，能删先删；删不掉的承载着用户在乎的事，按 AXIOM 5 演绎成 LEMMA/SPEC。
4. [AXIOM: 8] 避免大泥球架构。
    - 推理：大泥球是耦合与复杂程度的极端形态，已被 AXIOM 8 涵盖。
5. [AXIOM: 4, 8] 同一事实只留一个手写出处。缓存、生成物、文档副本必须机械再生，禁止手改。
    - 推理：AXIOM 4 要求最简实现，第二份手写副本不提供新功能；AXIOM 8 要求避免耦合，两份手写副本必须同步演化，同步一断就是分歧。手写一份，其余交给工具再生。
6. [AXIOM: 4, 7] 抽象要能指出当下的收益：消除的重复、隔离的边界（第二个使用方、测试替身、外部契约），或实测支撑的收益。指不出就先用具体实现，等第二个实例落盘再抽象。
    - 推理：AXIOM 7 要求复杂程度最低，AXIOM 4 要求最简实现。只服务一个使用方的抽象不消除任何重复，只加一层间接；第二个实例出现后，抽象才降低总复杂度。
7. [AXIOM: 4, 7; LEMMA: 3, 5] 例外集中管理，登记在同一处：兼容层、开关、废弃接口、做不到正交的耦合对。每项写清使用方与解除条件，条件满足即删。写不出使用方与解除条件的，不建；已建的现在就删。
    - 推理：LEMMA 3 要求删不掉的东西形式化，登记处就是形式化的落点；LEMMA 5 要求同一事实只有一处手写，例外清单就是那一处。AXIOM 7 要求复杂程度最低：分散的注释与 TODO 盘不过来，集中一处才能盘点、到期清理。写不出使用方的条目没有用户在乎，按 AXIOM 4 现在就删。

# SPEC
1. [AXIOM: 4, 7, 8; LEMMA: 4] 每个子文件夹是可正交编译的子模块，成立与否用两项检查判定：子模块能单独构建并跑自己的测试；子模块依赖图无环。做不到正交的耦合对集中登记（见 LEMMA 7）：谁依赖谁、为何。本文的结构即为落盘样例：命名就是 AGENTS.md，分布在各子文件夹，但 GUIDE 只有项目根目录一份。
    - 证明：子模块落盘后，逐个单独构建、跑测试、跑依赖图检查；当前仓库尚无子模块，两项检查空真；文件分布随时可直接查对。
