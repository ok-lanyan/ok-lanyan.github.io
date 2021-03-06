---
layout: post
title:  Web表单设计 -Luke Wroblewski
date:   2018-07-29
categories: 读书笔记
tags: 产品设计
---

* content
{:toc}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/01.jpeg"
    caption="" %}

# 一、表单结构
## 1.1 表单的设计
表单阻碍着用户需求（人们想从产品或服务得到东西）和商业目标（运营这些服务的公司希望基业长青），表单设计的重要性不言而喻。

- __由内而外设计__\\
根据数据库内部设计，直接请求“给我需要的信息”以便更新或创建记录，该请求就以表单形式出现在人们面前。

- __由外而内设计__\\
以组织会网站外部人的角度看待事物。

__1）衡量表单设计影响的方式__
1. 可用性测试\\
在可用性实验室中观察人们与表单如何交互，得到宝贵的定性和定量信息。
- 错误或问题的数量和位置
- 错误或问题的严重程度
- 完成率
- 完成整个或部分表单的时间
- 满意度评分
- 任务主观评论

2. 实地测试\\
从人种学角度观察人们在家中或办公室中与表单的互动情况。
- 访问表单，要求填写信息的来源：文档、软件和人等
- 表单的填写环境：吵闹的办公室和小监视器等
- 任何说明表单完成或错误率的额外情境

3. 客户支持\\
了解用户填写表单时碰到的问题，有利于分离和解决问题。
- 报告最多的问题
- 解决报告问题的常见方法
- 问题报告人的统计信息
- 问题报告人所使用的操作系统及其浏览器设置

4. 网站追踪\\
表单可用于追踪任意数量的有用量化指标。
- 完成率
- 如果表单未完成，人们是在哪个位置放弃填写的
- 人们访问表单的方式
- 已使用哪些表单元素
- 已输入哪些数据
- 浏览器和操作系统信息

5. 眼动追踪\\
记录人们如何理解表单的表现形式，用于解释复杂的地方。
- 人们在表单上看到了什么
- 眼球固定次数：解析表单所画的努力
- 眼球固定时间长度：看每个元素所花费的时间

6. Web惯例\\
调查表单设计问题的共同解决方案，可提供宝贵见解。
- 设计问题的独特解决方案
- 网上通用的模式

__2）设计原则__
- 尽量减少痛苦：填写过程应尽量简洁、容易。
- 说明填写完成的路径：应清晰告诉人们如何填完表单。
- 考虑情境：情境决定了如何使用表单。
- 确保一致沟通：表单是用户和公司间的中间人，多个团队（市场部、技术部等）参与对话，但表单只能用一种声音说话。

## 1.2 表单的组织
用户需要分析每个问题、想出答案、填空，加速该过程的最好方法是完全不要提问，因此应当测试每个问题：
- 一定要问吗？
- 能自动获得资料吗？
- 有没有更合适的时间或场所能得到答案？

你也许会恍然大悟表单中的问题原来是可以删除的。

__1）选取策略__

用户真正关心的是问题内容和所问原因，并且是否符合情境，是否与用户希望填完能获得的东西匹配。

思考人和关系，再思考在什么位置加入问题。例如为什么用户会填？用户和公司是什么关系？用户觉得这种关系是好是坏？表单能否进一步激发用户对产品、服务的持续热情？表单只是阻碍用户实现目的的可怕障碍？

以地址为例，如果在浏览商品前必须填写地址，用户会反感，可能会虚假回答或弃用，但如果在用户决定购买之后，需要填写地址，用户会小心、准确的填写。

四大策略，精准衡量使用：
- 保留：问题与用户渴望给出的答案匹配，那么留下并开始考虑设计细节。
- 删减：问题不需要得到答案，或能自动获得答案，那么删掉，减少用户工作。
- 延迟：问题不需要马上就问，延迟到不会让人感觉多余或有侵略性。
- 解释：用户不想回答、需要研究思考的问题，但对公司有价值，并有重要理由必须问，那么解释编写简短但清晰的理由，要确保能为用户带来好处。如果想不出，从头思考是否需要该问题，否则你将失去用户。

__2）构建对话__

以对话方式组织表单结构将有助于思考问题。

标签负责提出问题，输入框负责收集用户答案。

在构建对话时，需要留意以下问题：
- 考虑如何以对话形式而不是盘问形式组织表单。
- 标签是否通俗易懂，是否使用客户能理解的语言而非专业术语，如发卡行与哪家银行签发此文件，与哪家银行给的文件。
- 标签是否平易近人。
- 清晰明确的对话语言往往将有助于将问题解释清楚。

__3）组织内容__

根据问题数量和情景，将问题分成有意义的组，并分到多个或单个网页的不同部分。

理解每个表单的情境，谁要填？为什么要填？帮助我们将表单看作是与特定的人对话，主题之间就会自然出现间断。
- 如果主题鲜明简短，一个网页就能组织。
- 如果每部分都变长，可能需要多个网页把对话变成若干有意义的、可理解的主题。

Web惯例调查，比较相似网站的设计方案，观察特定领域中表现最佳的网站，以确保进行对比的网站采用共同成功措施。应当从发现的模式开始工作，而不仅仅停留于赋值竞争对手网站的做法。

__4）归纳区别__

内容组之间的差别不需要大量视觉差异。

事实上，内容组之间对比太多往往造成过多视觉污染，会阻碍人们浏览表单，无法聚焦在表单内容上，花费时间更长。

信息由产生作用的差异构成，任何无助于布局的视觉元素都会损害布局。因此，在考虑区分内容组时，应采用最少的视觉信息。

## 1.3 填写路径
__1）命名表单__

告诉用户，在填什么表单，填完之后能干什么。

用户采取的行动，保持一致至关重要，即表单名称与进入的子页面名称需要一致。

__2）起始页__

如果表单要求用户提供大量信息，而用户不可能有现成或大量时间来填写，起始页就能提供宝贵的情境信息：填写需要哪些信息、分几个主题步骤、整个过程大概多久。

只有需要花费大量时间的表单才考虑使用起始页说明路径。

__3）浏览线__

标签、输入框及主要动作按钮构成垂直轴，提供贯穿表单的单一路径。

设计良好的浏览线能恰当设置问题之间的视觉空间，不会错过任何重要信息。

一般，采用输入框高度的50%~75%作为问题之间的间隔。

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0101.jpeg"
    caption="- 虽然第一个表单内容组之间采用有意义的区分，但第二个提供了清晰路径，用户只需遵循向下的直线 -" %}

__4）最少分散注意力__

剔除与表单没有直接关系的界面元素，有助于用户完成填写表单任务。

额外元素对关键表单而言，最好的情况也会分散注意力，最坏时候造成用户不填写表单了。

__5）进程指示__

如果完成表单之前要回答的问题分散在多个网页，那么通过表单显示填表进展情况是很有用的。

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0102.jpeg"
    caption="- 显示范围、当前位置和状态的信息 -" %}

- 表单范围：总页数列表来说明，填完需要多长时间？每块内容与每步之间有何区别？
- 当前位置：相对于整个表单，用户所处位置。
- 表单状态：说明表单是否已提交以及上次保存时间，如果表单较长，提供保存或系统自动保存功能是保证用户填完表单的好办法。

如果表单没有清晰的有序网页，采用笼统、没有明确设置期望值的进程指示。

__6）Tab键跳转__

利用HTML的tabindex属性明确指定表单顺序。

大多数用户会使用Tab键在输入框间移动，混乱不堪的顺序会给用户很糟糕的体验。

# 二、表单元素
## 2.1 标签

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0201.jpeg"
    caption="- 左对齐、右对齐、顶对齐 -" %}

__1）顶对齐__

优点：
1. 眼球从标签移动到输入框50ms，填完表单最快捷的方式
2. 提供大量横向控件，适用于文字长度不一的扩大或收缩标签文字
3. 多个输入框可以组合在一行

缺点：
1. 占用额外垂直控件，不适用于垂直空间太少

__2）右对齐__

优点：
1. 眼球从标签移动到输入框240ms，能快速填完
2. 减少表单占用的垂直空间

缺点：
1. 左侧不齐，降低浏览表单文字的效率
2. 标签文字长度变化或需要两行字，浏览会更加困难
3. 标签长度和输入框组合的弹性较小

__3）左对齐__

优点：
1. 适用于收集用户不熟悉的数据，左对齐浏览表单文字更容易，不会被输入框打断
2. 减少表单占用的垂直空间
3. 适用于希望用户速度放慢，仔细考虑表单中每个输入框的情境

缺点：
1. 眼球从标签移动到输入框500ms，增加标签与输入框的距离，延长完成时间
2. 标签长度和输入框组合的弹性较小

__4）框内标签__

优点：
1. 减少一半表单的屏幕空间
2. 适用于只有一个问题（如搜索框）或几个输入框的表单（如通讯录）
3. 标签应清晰表明是标签，不是数据，如--Select Month--

缺点：
1. 填写时，标签消失，答题情境随之消失，突然忘记问题、检查答案比较难找回标签问题，不适用于表单问题较长的状况。

__5）混合对齐__

应当避免改变同一表单中的标签对齐方式，减轻一致性问题，因为不同对齐方式会模糊用户寻找完成表单的明确路径。

## 2.2 输入框
输入框的类型有文本框、单选框、复选框、下拉框、列表框5种。

输入框的长度：可以暗示填表时有用的线索，答案长度与输入框长度是否匹配，但最好不要让用户考虑太多，而如果无法受益于暗示，就应当采用一致的长度。

必填项：建议在少数问题可选或必填项上，用文字optional/required来代替*，放在标签文字的后面，而不是输入框后面。

## 2.3 动作
主动作：完成表单填写是最主要行为

次动作：与完成表单填写相悖的行为

__1）如何区别主动作与次动作？__

我们的目标是，减少次动作的视觉表现，潜在出错率降到最低，并进一步引导用户成功填完表单。

那么主动作与次动作在表现形式上应当有多少差异？

用绿色标识主动作或图标、红色标识次动作或图标，能有效区别两者。因为红色与错误密切联系，常被用来说明不好的事情。

谨慎放置表单动作，主动作和输入框对齐会减少填写表单的时间。

__2）如何避免重复提交？__

主动作前，提醒用户不要点击两次，会加重用户负担，可以用动画和提交中的文本信息代替，过程会变得更清晰。

在填写符合要求前，禁用并可见主动作，但如果表单含有可选问题时，应避免该方法。

__3）同意协议和主动作的处理__

大多数表单都带法律条款，确保新会员同意。

“立即注册”与“同意并立即注册”，好处是用户少回答一个模棱两可的问题。

将协议和提交分为两个元素，复选框确认协议，按钮完成表单，复选框未勾选，禁用主动作。

## 2.4 帮助文字
帮助文字，基本上是一套帮助用户成功填表的信息。

当用户不懂专业术语、质疑为什么要填、关心隐私安全问题、系统推荐填写方式（如逗号分开标签）、少数可选或必填时，需要在毗邻输入框处，放置简洁清晰的帮助文字。

动态帮助系统，自动触发或通过明确的用户操作进行访问，解决帮助文字超过表单长度的问题。
- 帮助文字出现在右侧：总是出现在输入框右侧，但与输入框完全没有关系，是对标签的说明。
- 帮助文字悬浮出现：很容易与问题产生联系，但会遮住其他输入框。
- 帮助文字用于输入组：适用于一组相关输入框。

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0202.jpg"
    caption="- 帮助文字出现在右侧 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0203.jpg"
    caption="- 帮助文字悬浮出现 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0204.jpg"
    caption="- 帮助文字用于输入组 -" %}

但动态帮助系统有一个潜在缺点，只有开始填表时，用户才知道是否有帮助文字。而需要帮助的用户会觉得失望，不愿意尝试。可以采用输入框内显示帮助文字的方式（hint）。

用户如何激活动态帮助系统
1. 鼠标指针连续保持在触发热点500ms，显示悬浮帮助框，如果指针离开，帮助框消失。。
2. 点击弹出帮助新窗口，但窗口拦截器导致不够理想。
3. 开辟毗邻相近固定区域，显示帮助内容，受帮助文字长度和个数限制较多，不好布局。
4. 右侧帮助面板，可隐藏、可更新内容。

## 2.5 错误与成功
- 错误消息：不能被忽略或置之不理，必须要解决错误。
- 成功消息：不能阻碍用户进程，鼓励用户采取更多行动。

__1）双重视觉强调__

标签和输入框置为红色，同时在输入框下方增加红色指导文字。只改变标签颜色，不足以引起色盲人士的注意。

确定了一种视觉处理方式来表现输入错误，应确保该风格匹配表单上任何主要错误消息，有助于人们找到相关点。

__2）多个错误或错误不是某个特定输入框产生__

1. 突出消息，表明发生错误
2. 双重视觉强调每个产生错误的输入框
3. 同时在两处（顶部和出错的输入框处）给出清晰的解释和操作，帮助用户迅速解决错误
4. 当表单较长，发生错误的输入框在可见区域之外时，跳到表单的第一个错误处。

__3）成功消息__

应当确保用户知道成功填完表单，并快速给予用户应得的表扬。

成功消息不能阻碍进程，自动移除是合适的做法，最好采用动画形式，如渐变、融化、滚动等。

__4）消灭死胡同__

成功消息，还应包括刚完成任务关联的有用后续操作，明确告诉用户下一步该做的事情，永远不要丢下用户不管！避免页面成为死胡同。

# 三、表单交互
## 3.1 即时校验
即时校验，在输入开始、继续、停止的时候，直接反馈有助于确保用户回答有效。

__1）确认答案正确性__

在当前输入框填写有值并移入下一个输入框时，对该答案进行验证，将信息实时更新并反馈给用户，防止用户陷入错误循环。同时，也能避免主动作一次性校验所有输入框，分散注意力，引起部分用户的反感。

信息，应简单易懂，甚至告诉用户修改的方法，起到引导的作用。

比如，“用户名已被占用，试试加上数字”、使用密码强弱尺引导用户设置安全性更高、更复杂的密码代替“从内而外”设计的移入下一输入框时的即时校验。

__2）自动补全提供即时建议__

如果有一组特定答案都有效，但范围太大，无法设计成简单的用户界面，此时，自动补全能确保用户提供有效答案。

比如，机场代码，可能知道部分答案，然后输入“ord”就会出现一组有效答案，用户选择即可。

__3）限制输入框的输入内容__

有些问题没有明确定义的答案，但有明确定义的限制。限制后，有助于避免潜在错误。

比如限制输入框字数、输入数据类型等。

## 3.2 多余输入
要小心设置每个问题，如果某个问题并非必要，要么去除，要么在更好的时间或位置提出，要么自动推断出答案。

提的问题越少，用户就能越快越容易填完表单。

应付无处不在的过多选择，采用智能默认帮助用户做出明智选择，减少必要的选择次数。

如默认勾选同意捐赠器官、根据身份证号默认性别、根据访问IP默认国家等等。

但智能默认会诱使公司更多考虑商业，较少为用户考虑，如有可能，应当确保符合用户利益。

个性化默认，保持用户之前的选择。某个选项被选择多少次后，就设为个性默认选项，减少用户操作次数。

## 3.3 额外输入
__1）高级选项__

点击按钮，动态添加删除视图，提供给需要的人，同时不阻碍不需要的人。\\
页面跳动会导致表单已有内容下移，扰乱用户对所处位置的感知，应当减少表单页面的跳动次数。

__2）叠层对话框__

额外输入框出现在表单上方。

__3）静态叠层窗口__

在额外输入需要单独关注时使用，并确保不会遮住输入框。弹出时，表单其他部分本质都被禁用，只能修改额外输入框。

__4）类别选择器__

如父子类别的选择器、省市区选择器等。

## 3.4 基于选择的输入
基于选择的输入：根据用户的回答，出现一系列要回答的后续问题。而出现什么问题基于最初的选择。

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0301.jpg"
    caption="- 水平选项卡 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0302.jpg"
    caption="- 垂直选项卡 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0303.jpg"
    caption="- 下拉列表 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0304.jpg"
    caption="- 单选按钮下方显示 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0305.jpg"
    caption="- 单选按钮内显示 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0306.jpg"
    caption="- 显示非活动选项 -" %}

{% include image.html
    img="/styles/images/2018-07-29-web-table-design/0307.jpg"
    caption="- 组的显示 -" %}

__页面级选项__

采用两个单独的网页，第一页显示初始选项，用户选择其中一个，就会出现相关的选择性输入，取代初始选择。

类型 | 优点 | 缺点
- | - | -
页面级选项 | 1. 初始选择和相关输入关系明确<br> 2. 适用于相关输入数量很多的情况 | 1. 一旦做出初始选择，两步就会失去宝贵的情境关系
水平选项卡 | 1. 没有参与者出错，能够迅速完成任务，且打出了满意度最高分 | 1. 选项卡之间是否互斥、提交选择是针对所有选项卡还是当前选项卡不够清晰<br>2. 偏离填表过程中清晰的线性扫描，阅读选项卡时，需要额外努力
垂直选项卡 | 1. 眼睛固定总时长最短、平均固定时长最短、平均固定次数最少，表现最佳<br> 2. 确保选择后，眼睛不需要太多移动，更有效率 | 1. 选项卡是否互斥有困惑，可添加单选按钮传达互斥含义
下拉列表 | 1. 表现平均，满意度较高，只有1人出错<br> 2. 适用于初始选项数量较长（4或5个以上）的情况 | 1. 随着选项增加，很难保持相关输入很好的比例
单选按钮下方显示 | 1. 更清晰表明两步的情境关系<br>2. 适用于少量相关输入和动画过渡 | 1. 如果用户改变选项、刷新时，页面跳转效果会导致用户迷失方向，尤其是额外输入很长时<br> 2. 单选按钮与相关输入之间的视觉间隔，会给用户带来更多视觉上的不适
单选按钮内显示 | 1. 速度最快，平均固定次数最少，但有几个人出错<br> 2. 适用于少量相关输入和动画过渡 | 1. 页面跳动+初始选项移动，造成交互失去方向，用户频繁困惑于哪个选项触发哪套选项
显示非活动选项 | 1. 所有相关输入可见，保留初始选项的情境 | 1. 所有相关输入可见，给用户带来困惑，初始选项之间丧失联系；<br> 2. 表现最差，必须关闭不需要填写的相关输入
组的显示 | | 1. 可视化分组很快降低初始选项的可见度，出错最多，应避免使用

## 3.5 循序渐进
循序渐进：在用户了解产品主打服务后再注册。

考虑一系列交互如何向潜在用户说明如何使用以及为什么要使用你的服务，来判断该产品是否适合循序渐进。

但如果只是把注册的输入框拆分到不同页面，就不要使用循序渐进。因为可能会降低效率，也使用户感觉不快。
