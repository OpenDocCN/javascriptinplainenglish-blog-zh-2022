# 如何将机器学习添加到 Node.js 应用程序中

> 原文：<https://javascript.plainenglish.io/how-to-add-machine-learning-to-your-node-js-app-720bb98e4721?source=collection_archive---------4----------------------->

## 原来你可以用 JavaScript 来使用机器学习。

![](img/88aea2219b9bc02ca67e749de9e39565.png)

*最初发布于*[*https://fek . io*](https://fek.io/blog/how-to-add-machine-learning-to-your-node-js-app/)*。*

我正在尝试学习更多关于机器学习的知识。当你听到像多层神经网络和线性回归这样的术语时，人工智能和机器学习在表面上可能会显得令人生畏。但是对于简单的任务，您可以使用浏览器或 Node.js 轻松利用机器学习。

我目前每天收到数百封电子邮件。这些电子邮件中有很多要么是时事通讯，要么是技术出版物，它们会向我感兴趣的故事发送超链接。我最感兴趣的头条是编程相关的。我一直在寻找方法来简化这些邮件，以便找到我想看的标题。所以我决定使用 Node.js 通过机器学习来解析我的电子邮件。

# Node.js 是机器学习的最佳语言吗？

简短的回答是**没有**。也就是说，我选择这种语言是因为我已经很熟悉它来编写我自己的家庭自动化。如果你真的想学习人工智能和 ML，Python 是一个更好的开始语言，因为有大量的资源和框架来做这种类型的计算。

一些流行的 ML 工具有 Keras，TensorFlow，NLTK，PyTorch，Scikit，Pandas，Numpy 和 MXNet。我提到的还有很多。

对于 Node.js，我使用了几个不同的模块，包括 [TensorFlow.js](https://www.tensorflow.org/js) 、 [Brain.js](https://brain.js.org/#/) 、 [Natural](https://github.com/NaturalNode/natural) 和 [ML-classify-text](https://github.com/andreekeberg/ml-classify-text-js) 。我最终选择了 Natural，因为我想做的是将标题归类为我可能感兴趣阅读的特定主题。

# ML 工作流

机器学习工作流程可以分为几个步骤。第一步是找到构建模型的最佳算法。对于文本分类，我在寻找一些非常简单的东西。Natural 有几个不同的分类器，我选择了 BayesClassifier。

下一步是查找或定义可用于训练模型的数据。对于我的项目，我使用了以前的标题，这些标题是我已经为我感兴趣的主题领域选择的。这一步可能是最重要的。您拥有的数据越多，数据越精确，您的模型在选择正确的分类时就能表现得越好。

训练完模型后，下一步是测试模型与实际数据的准确度。

最后一步是将您的模型部署到应用程序中。一些 ML 框架允许模型在创建后被更新。这很好，因为随着时间的推移，您可以继续迭代您的模型，使其更加精确。

# 自然的例子

下面的例子来自自然源代码的例子，但是它给出了一个设计、训练和使用一个模型是多么容易的想法。

一旦您训练了您的模型并测试了它的有效性，您将需要保存它以便您可以在您的应用程序中重用它。这是一个如何使用 Natural 保存模型的例子。

一旦保存了模型，就可以使用下面的函数重新加载它。

保存和加载功能都是异步任务。如果您想以更同步的方式加载您的模型，您可以在现代 JavaScript 中使用 async/await。

# 硬件要求

我们在这篇文章中使用的 NLP 或自然语言处理不需要大量的计算能力，但如果你想进入深度学习和图像识别，你会想研究 GPU 和其他专门的处理器。许多框架都有利用这些类型处理器的硬件加速。

Nvidia 有一个名为 [CUDA](https://developer.nvidia.com/machine-learning) 的库，让开发人员利用他们的硬件来做加速机器学习所需的线性代数。

谷歌也有一个处理器，他们称之为 [TPU](https://cloud.google.com/tpu/docs/tpus) ，或张量处理单元。这是一款专门设计用于使用专用集成电路或 ASICs 处理张量的处理器。

苹果公司的 M1 处理器也有一部分专门用于 ML 任务，称为神经核心。在现有的 ML 框架中使用 M1 的一个注意事项是，许多现有的项目都依赖于 Python 2.7。Python 2.7 将不得不在 M1 MAC 电脑上的 Rosetta 2 下运行。有一些框架利用了 M1s 中的神经核心，但您必须研究这是否能满足您的需求。

# 结论

将 ML 添加到 Node.js 项目中相当容易。值得花一些时间来了解一些其他可用的 ML 框架，如 Brain.js 和 TensorFlow.js。这些框架可以做一些高级的事情，如构建神经网络和进行图像分类。想想`Hotdog/Not Hotdog`。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*