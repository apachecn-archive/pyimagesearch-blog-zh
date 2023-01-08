# 计算机视觉和野火探测专家大卫·波恩访谈

> 原文：<https://pyimagesearch.com/2021/10/13/an-interview-with-david-bonn-computer-vision-and-wildfire-detection-expert/>

想象一下:

你在乡下建了一个全新的家，远离大城市。你需要远离喧嚣，想让自己回归自然。

你建的房子很漂亮。晚上很安静，你可以看到星座在天空跳舞，你睡得很好，知道你会醒来休息和恢复活力。

然后，你在半夜醒来。抽烟？*有火吗？！*

你跑下楼梯，来到门廊上。在地平线上，你会看到橙色的光芒，仿佛整个天空都着火了。浓烟滚滚，就像一个愤怒的风暴云准备窒息你。

**果然，是野火。根据风向判断，它正朝你吹来。**

你美丽宁静的家现在变成了一场易燃的噩梦。

你不得不怀疑……计算机视觉是否可以在早期被用来探测这场野火，从而向该地区的消防队员发出警报？

不过现在没时间想这些了，只要拿起你能拿的贵重物品，扔到卡车后面，然后离开那里。

当熊熊大火逼近你的房子时，你最后看了一眼后视镜，发誓总有一天你会发现如何及早发现野火…然后你开着车在一条土路上寻找文明。

恐怖故事，对吧？

虽然我为了戏剧效果对它做了一些修饰，但这和大卫·波恩在华盛顿州的家中多次经历的事情没有什么不同！

大卫在过去几年的职业生涯中致力于开发一种早期预警计算机视觉系统来检测野火。

该系统运行在 Raspberry Pi 上，并通过 WiFi 或蜂窝调制解调器连接到互联网。如果检测到火灾，RPi 会 pings David，之后他可以向消防部门报警。

此外，美国专利局刚刚授予大卫多项专利！

今天很高兴大卫来到了 PyImageSearch 博客。他是社区论坛的长期读者、客户和版主。

最重要的是，他的工作有助于防止伤害和生命损失，这可以说是最臭名昭著的难以早期发现的自然灾害之一。

**要了解大卫·波恩是如何创造出一种计算机视觉系统来探测野火的，请继续阅读完整篇访谈！**

## **采访计算机视觉和野火探测专家 David Bonn**

阿德里安:嗨，大卫！感谢您抽出时间接受采访。很高兴您能来到 PyImageSearch 博客。

大卫:谢谢你，阿德里安。和你聊天总是很愉快。

* * *

阿德里安:在我们开始之前，你能简单介绍一下你自己吗？你在哪里工作，你是做什么的？

大卫:从大学开始，我就断断续续地从事开发和工程师的工作。在这些工作之间，我做过各种“有趣”的工作，比如公园管理员、河道向导、滑雪教练和火灾了望员。

1996 年，我和其他几个人一起创建了 [WatchGuard Technologies](https://www.watchguard.com) ，它取得了巨大的成功，事实上，今天它仍然存在并保持独立。那次冒险之后，我处于半退休状态，四处旅行。在同一时期，我花了很多时间从事环境教育项目和其他自然历史项目。

这些天来，我一直在努力创办一家新公司——Deepseek Labs。

* * *

**Adrian:** 是什么让你对研究计算机视觉和深度学习产生了兴趣？

大卫:大约十年前，对我来说很明显，神经网络及其工作方式发生了巨大的变化。他们终于走上了拥有可以解决实际问题的工具包的道路。对我来说更有趣的是，有一大类真正的问题，你可能无法用更好的方法来解决。

几年后，我开始涉猎 OpenCV，主要是通过下载书籍和浏览它们的例子，然后我在 2015 年偶然发现了你的博客。

2014 年和 2015 年，我家附近发生了一系列大规模野火。虽然我的家毫发无损，但近 500 所房屋在大火中被毁，几名消防员牺牲。我想到这里有一个巨大的未解决的问题，我想知道我能做些什么来解决它。

2017 年末，我发现自己处于这样一种情况，人们需要评估他们的生活以及他们在做什么。与此同时，我与朋友和邻居就野火问题以及我们需要什么工具来适应这种新情况进行了多次交谈。

在这些对话中，我脑海中闪现的一件事是(大约)，*“天哪，难道我不能制造一些能够探测火灾并在几分钟内警告人们逃命的东西吗？”*因此，我决心学习足够多的计算机视觉和深度学习知识，以弄清楚这样的事情是否可能实现。

通常，我发现如果你希望掌握一项新技能，如果你头脑中有一个项目(或一系列目标)需要这项新技能来推动你前进，会有很大帮助。所以我掌握计算机视觉和深度学习的项目是建立一个简单但实用的火灾探测系统。

* * *

**Adrian:** 我与你互动的最初记忆之一是在 PyImageSearch 社区论坛上，你在那里讨论火灾/烟雾探测，以及在你居住的地方这是一个多么大的问题。这些野火是如何开始的，为什么早期发现如此重要？

大卫:每场火都不一样。现在，在我家 30 英里范围内有 4 处大火。三起是由闪电引起的，一起是由一个在灌溉泵上工作的人引起的。通常情况下，美国的大多数“野火”都发生在由人类活动引起的相当发达的地区。这可能是任何事情，从树枝上短路的电线，到在干草中空转的车辆，到某人在篝火上不小心煮热狗。

从成本和公共安全的角度来看，早期检测非常重要。扑灭一场小火可能要花费几千美元。一场大火很容易造成数千万美元的损失。我家附近的 Cub Creek 2 火灾，高峰期有 800 多人救火。一辆[刷车](https://skeeterbrushtrucks.com)里的一个小团队每天可能要花费 1000 美元，而一架大型直升机通常每小时要花费 8000 美元。这些费用迅速增加。

此外，虽然大多数人都可以用铲子和水桶安全地扑灭营火，但扑灭大火更像是抗击天气现象。你也许可以让它慢下来或者稍微控制一下，但是你不可能停止它或者完全压制它。

可能在我附近燃烧的火还会在某个地方燃烧，直到 11 月开始下雪。但是，随着大量的灌木丛被大火清除，今年冬天滑雪可能会很棒！

强调早期发现的另一个重要原因是，许多“野火”始于人们居住的地区。如果给人们几分钟时间安全疏散，早期检测可以挽救生命。在美国西部和加拿大，大约有 450 万个家庭处于野火的高风险或极端风险中。

* * *

阿德里安:几周前，你自己的家受到了野火的影响。你能告诉我们发生了什么吗？

大卫:我可以从我的角度告诉你发生了什么。

一个重要的背景:我住在华盛顿州的中北部，尽管华盛顿的名声在外，但这是一个非常干燥的地方，夏天经常非常温暖。这是一个极其干燥的春天(该州东部的大部分地区正处于严重的干旱之中)，而且我们在六月下旬经历了一场令人难以置信的热浪。所以植被非常干燥。有多干？嗯，火灾研究人员从树上提取核心样本来评估燃料的干燥度。火灾前两周在我所在的地区采集的岩芯样本发现，活树比窑干木材干燥，含水量约为 2%。典型的纸张含水量为 3%。

7 月 16 日星期五，白天最热的时候，我在家，也在屋里。大约下午 1 点 45 分，我向外望去，注意到南边有一股不祥的烟柱。就在那时，我出去了，从烟的方向吹来了一股相当强劲的风。

那时，大量的练习和计划开始了。我迅速关闭了所有的窗户(大多数已经关闭)。入口里有一包衣服、一箱文件和硬盘，我很快就把它们装进了卡车。然后我把四只狗都带上了卡车。最后看了一眼房子，我向山下走去，与此同时，我开始给我的邻居发短信，告诉他们火灾的情况，并鼓励他们离开那里。

在这一点上，我和我所有的邻居都非常幸运。在区域[有另一场大火，他们立即将消防队和飞机转移到这场新的火灾中。因此，在一个小时内，有几架飞机和大约 100 名消防队员到达现场(当消防队员到达现场时，火灾已经估计有 1000 英亩大小)。](https://inciweb.nwcg.gov/incident/7655/)

附近还有一名重型设备操作员，甚至在所有消防员到场之前，他就在用推土机到处切割火线。

我的邻居和消防队员们的快速行动产生了一个近乎奇迹的结果:只有几栋建筑受损，其他几栋也有轻微损坏。没有人受伤或死亡。

尽管有一个全县范围的紧急警报系统，我们没有一个人得到任何警告——来自县系统的警告在下午 2:30 左右到达我的手机。如果这一系列事件发生在凌晨 1 点 45 分，而不是下午 1 点 45 分，事情会更加悲惨，肯定会造成房屋和财产的损失，也可能会造成生命损失。

有趣的是，当这一切发生时，我有一个原型火灾探测系统在外面运行。当然，当它探测到火的时候，我已经在相当远的地方了。不幸的是，当它检测到火灾时，WiFi 已经关闭(当我撤离时，我家停电了，第二天很晚才恢复)。因此，我无法保存任何检测图像。此外，探测器本身是靠零目标电池组运行的。

* * *

阿德里安:你和你的公司开发了一种可用于农村地区的火灾探测系统。你能告诉我们解决方案吗？它是如何工作的？

**大卫:**30 秒的答案是，我使用热感相机( [FLIR 轻子 3](https://www.flir.com/products/lepton/) )和基本的 OpenCV 图像处理功能来寻找好的候选区域。我传递给另一个程序，该程序用光学相机检查这些区域，然后将光学图像的切片传递给二元分类器。

更长的答案是，热感相机寻找两个靠近的东西:热点(热感图像中非常明亮的部分)和湍流运动区域。因此，如果我可以在一个非常热的点附近找到湍流运动，并且湍流运动主要在该热点上方(记住*热空气上升*)，热点和湍流运动重叠的区域(或者如果适当扩大它们重叠的区域)是找到火焰的可能位置。

然后，光学算法获取该候选区域，并将它们的坐标转换到光学相机的坐标系。因此，通过仔细观察候选区域，我可以选择光学图像中适合传递给训练有素的二进制分类器的良好切片。

我的一个重大发现(嗯，对我来说，这是一个重大发现)是，虽然有一个很好的数据集和一个良好的网络，但如果你的分类器正在查看一幅图像的精心选择的切片，你可以获得 96-97%的准确率，准确率高达 99%以上。我怀疑通过精心构建的集合，你可以达到更高的精确度。

如果热算法和分类器都同意有火灾，则系统进入报警状态。

该系统本身的准确率超过 99.99%，这意味着在样品(户外)中运行时，每 3-5 天就会出现一次“错误”。样本外(例如，在我的厨房里用煤气灶)每天会出现 4 到 5 次错误。使用帧平均或系综可能会有更高的精度。由于热图像的分辨率(160×120)和帧速率(9 fps)在大多数情况下都非常低，因此该系统不必非常努力就可以获得这些令人印象深刻的结果。

我使用的方法远非完美，在某些情况下仍然很困难。内燃机，尤其是重型设备或农用设备的热废气经常会扰乱热算法。分类器与明亮的主题斗争，甚至更明亮的背光主题。靠近传感器的色彩鲜艳的鸟有时会产生令人困惑的结果。随着时间的推移，通常通过收集更具代表性的训练数据，这些问题正在得到缓解。

我已经为这个系统的许多部分申请了专利，8 月 11 日，我被告知那些专利是允许的。在更多的费用和文书工作之后，这些专利将被正式发布和出版，然后我可以分享更多关于该系统如何工作的细节。

* * *

阿德里安:你们的火灾探测系统运行在什么硬件上？你需要一台笔记本电脑/台式机，或者你正在使用类似树莓派，杰特森纳米等。？

大卫:核心火灾探测器运行在树莓派上。现在的参考实现是 Pi 3B+,检测时间大约为 1-2 秒。目前，该系统要么通过 WiFi 连接到互联网，要么使用[蜂窝调制解调器](https://sixfab.com/product/raspberry-pi-4g-lte-modem-kit/)。我的首选是使用蜂窝调制解调器，因为我们可以自行配置系统，并在没有任何最终用户设置的情况下启动和运行它。

我正在引导只读的 Pi。这使得该系统在面对断电和其他故障时更加稳健，但不可能将检测图像直接保存在 SD 卡上。

这个系统的其他部分将在云上运行，也将有一个客户端(网页或应用程序)，可以向您显示部署的检测器，它们部署在哪里，以及它们的状态如何。

* * *

**Adrian:** 将红外摄像头与“标准”图像处理和 OpenCV 代码结合起来，最难的是什么？你遇到了哪些拦路虎？

大卫:对我来说，最大的障碍是让硬件工作起来。GitHub 上有许多硬件障碍(包括不支持和不推荐的部分)和许多过时的代码，我必须努力克服。我终于找到了一些还算过得去的代码，至少让我可以开始了。例如，普通的轻子分线板使用 I2C，所以你有一堆电线连接到你的 Raspberry Pi 上的 GPIO 总线。我让所有这些工作，但它不是探索更好的火焰检测算法的最佳环境。

当我切换到使用一个 Purethermal 2 USB 模块时，我的进度大大提高了。这是一个巨大的进步，因为只需很少的努力，我就可以在笔记本电脑上试验热感相机的图像处理算法。因此，与其将代码上传到 Pi 并重新启动 Pi，然后在另一个显示器上查看输出，我可以只在我的笔记本电脑上进行代码-测试-调试循环，然后在我的办公桌上、厨房的桌子上或面包店工作。因此，我很快就在这个系统上花了更多的时间，并且在一个月内学到了比过去六个月还多的东西。

一旦你与硬件对话，真正的工作就开始了。轻子是一种非常敏感的仪器，它只有 160×120 的空间分辨率，但每个像素都是 16 位深——像素值的 1 位变化代表大约 0.05C 的温度变化。这足够敏感，如果你赤脚走在寒冷的地板上，你的脚印将在热成像中“发光”几分钟。另一方面，许多 opencv 函数并不真正喜欢 16 位灰度图像，所以您需要小心您调用的函数，并且您可能需要使用 numpy 进行一些操作。

你需要注意的最后一点是热图像的对比度非常低。因此，除非您以某种方式增强它们(通常归一化直方图就足够了)，否则当您显示图像时，您将看不到任何有趣的东西。

* * *

阿德里安:你认为你从建立火灾探测系统中学到了什么？

**大卫:**简答:很多！

我认为(到目前为止)最大的收获是，你应该期待花很多时间来构建伟大的数据集。你不应该期望它是容易的，你应该期望一路上会有很多试错和学习的经历。然而，一旦你开始构建一个伟大的数据集，并有一个框架让你不断改进它，你就处在一个奇妙的地方。

在你的文章中，你大谈高质量数据集的价值。那是百分之百正确的。然而，我会更进一步说，如果您构建了一个框架和流程，让您可以轻松地增长和扩展数据集，那么您正在创造更有价值的东西。

* * *

**Adrian:** 您在构建火灾探测系统时使用了哪些计算机视觉和深度学习工具、库和软件包？

David: 我使用了 OpenCV、Tensorflow、Keras、picamera 模块和您的 imutils 库。

* * *

阿德里安:你在这个项目中的下一步是什么？

大卫:我们现在正在做两件事:第一件是我们有一些原型，我们正在花时间研究它们，了解我们正在使用的方法的局限性以及如何使它变得更好。与此同时，我们正在与潜在客户交谈，向他们展示我们所拥有的，并谈论我们的想法，并试图找出如何解决他们的问题。

我们学到的一件大事是，如果你能在一个社区周围部署许多(至少几十个，可能几百个)火灾探测器，整个想法会更好。然后，你可以给人们一个网站或一个应用程序，让他们回答他们关心的问题:*火在哪里？*

* * *

阿德里安:你是 PyImageSearch 的长期读者和顾客。谢谢你支持我们！(还有*更感谢*成为社区论坛中非常有用的版主。)PyImageSearch 对你的工作和公司有什么帮助？

**David:** 我可以接触到更明智、更有经验的人(你和 Sayak Paull 都非常有帮助)，他们可以在我陷入困境时帮我解决问题(当我切换到 Tensorflow 2.x 和 tf-data 时，我有几次都搞砸了，你和 Sayak 都在帮我找出问题所在方面发挥了巨大作用)。

我喜欢参与 PyImageSearch 的另一点是，帮助他人是提高自己技能和学习新事物的好方法。所以对我来说，这是一次很棒的经历。

* * *

Adrian: 如果一个 PyImageSearch 的读者想和你联系，他们该怎么做？

**David:** 与我联系的最佳方式是在我的 LinkedIn 上，地址是 [David Bonn](https://www.linkedin.com/in/david-bonn-427449b/) 。

## **总结**

今天我们采访了大卫·波恩，他是利用计算机视觉探测野火的专家。

大卫已经建立了一个专利的计算机视觉系统，可以成功地检测野火，使用:

*   树莓派
*   前视轻子热感相机
*   蜂窝调制解调器
*   专有 OpenCV 和深度学习代码

该系统已经被用于探测野火和向消防队员发出警报，防止人员伤亡。

早期野火检测是计算机视觉和深度学习如何彻底改变我们生活几乎每个方面的又一个例子。作为计算机视觉从业者，大卫的工作展示了我们的工作可以对世界产生多大的影响。

我祝 David 好运，因为他将继续开发这个系统——它确实有潜力拯救生命，保护环境，并防止巨大的财产损失。

**在 PyImageSearch、** ***上发布未来教程和采访时，您只需在下面的表格中输入您的电子邮件地址即可获得通知！***