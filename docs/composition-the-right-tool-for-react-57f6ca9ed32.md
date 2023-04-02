# 合成:React 的正确工具

> 原文：<https://javascript.plainenglish.io/composition-the-right-tool-for-react-57f6ca9ed32?source=collection_archive---------13----------------------->

## 了解什么是构图以及何时使用构图——用例子解释。

![](img/3168db315961b71983d2a6a44d3ddc47.png)

Photo by [Julia Kadel](https://unsplash.com/@juliakadel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我第一次开始学习 React 时，我努力制作一些可重用的组件或避免创建太多特定的组件，这在我的项目中是一个大问题，直到我学习了 composition。

构图是一个非常众所周知的概念，但有时解释只是肤浅地涵盖了这个概念隐藏的真正力量。在这篇文章中，我将向你展示许多具体的例子，在这些例子中，组合是一个巨大的胜利，并且根据什么时候使用组合是一个好主意，什么时候我更喜欢使用另一种策略，给出一些个人意见。

## 什么是作文？

组合是一个非常简单的概念，不仅在 React 中使用，在一般编程中也使用。例如，您可以组合许多函数:

```
def sum(a, b):
  return a + bdef pow2(a):
  return a * adef getScore(a):
  return sum(a, 2) + pow2(a)
```

简而言之，您可以组合许多函数(sum 和 pow2)来产生第三个函数(getScore ),该函数使用低级函数来产生更高级别的结果。

**这种情况下为什么要用构图？**

另一种方法是创建一个函数，只完成你需要的工作，例如:

```
def getScore(a, b):
  return a * a + b * 2
```

**出现的问题**

*   当所有的实现只存在一个大函数时，推理就更具挑战性了。
*   测试一个大功能比测试几个小功能更困难。
*   遵循单一责任原则，每个职能只有一个改变的理由。当问题被分解成小函数，每个函数只关注一个问题时，这种情况更为真实。
*   如果你做同样的过程得到某个数的幂或者复制一个数，你需要重新实现逻辑。

**注。**这只是一个简单的例子，说明合成术语不仅仅是反应，它是一个更抽象的概念。

## 反应中的成分

![](img/51538078ca8ed05cf626f1395bf4c1f6.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 react 中，您可以以稍微不同的方式使用复合。要使用构图，首先，重要的是要知道它是什么`children`道具。

默认情况下，所有 React 组件都会收到一个参数，按照惯例，该参数通常被命名为 props。这个参数总是有一个名为`children`的特殊属性，这个属性包含当前组件的内部标签中传递的所有组件，例如:

```
function Grid (props) { }function Item (props) { }# ...
# Inside another component
# ...
<Grid>
 **<Item/>
  <Item/>  // Components inside the Grid component, they are refered
  <Item/>  // as props.children in the Grid component**
</Grid>
```

在这种情况下，`Grid`组件中的`props.children`将成为一个包含三个类型为`Item`的元素的对象数组。

了解子属性并不总是数组类型非常重要，例如:

```
<Grid />                              **# props.children = Undefined**
<Grid><h1>Title<h1></Grid>            **# props.children = Object**
<Grid><h1>Title1</h1><h1>Title2</h1>  **# props.children = [Object, Object]**
```

**注意。**重要的一点是，所有的组件可能不会只返回`undefined`作为值，所以当你的函数只返回`props.children`的值时要小心，因为在这种情况下，`props.children`应该是强制的。

**构图的简单情况**

现在，在 react 中，你用 HTML 标签创建一个组合，例如，在这个例子中，我用`h1`和`p`标签组成了`div`标签。

```
function HomePage = () => {
  return (
    <div>
      <h1>Home page</h1>
      <p>Content of page<p/>
    </div>
  )
}
```

这个想法可以用你自己的组件来扩展。

```
**function Container() { ... }
function Paragraph() { ... }**function HomePage = () => {
  return (
    <Container>
 **<Heading>**Home page**</Heading>
      <Paragraph>**Content of page**<Paragraph/>**
    </Container>
  )
}
```

在这个简单的例子中，优势并不明显，但现在我们将看到一个现实的例子，尤其是当您利用自定义组件和`children`道具时。

## 实践写作

假设您有一个需要在屏幕上显示的文章列表。在第一个实现中，您决定创建一个`ListArticle`组件，它在内部定义了`className`来生成布局，在本例中，是一些网格(1)，同时定义了网格将包含一个`ArticleCard`组件列表(2)。

```
function ArticleCard(props) {
  # Show the information of the article in a card
  return (
    <div className='article-card'>
      article: props.article.name
    </div>
  );
}function ListArticle(props) {
  # Show a grid of articles
  return (
    <div **className='article-grid'**>                            **// (1)**
      **{props.articles.map(a => <ArticleCard article={a} />)}  // (2)**
    </div>
  );
}
```

这听起来很棒，但存在一个主要问题。如果你的文章是从一个外部 REST API 获取的，有可能你想在获取数据的同时显示[骨架](https://chakra-ui.com/docs/components/feedback/skeleton)网格，所以，你被迫创建两个新组件。

```
function ArticleCardSkeleton(props) {
  return (
    <div className='article-card-skeleton'>
      ...
    </div>
  );
}function ListArticleSkeleton(props) {
  return (
    <div **class='article-grid'**>            **// (1)**
      **<ArticleCardSkeleton />             // (2)
      ...
  **  </div>
  );
}
```

但是你看到问题了吗？。`ListArticleSkeleton`与`ListArticle`组件非常相似，网格布局 **(1)** 都是一样的，唯一的变化是它里面的组件类型 **(2)** 。你可能会开始认为这种方法有问题，是的，有可能做得更好，你只需要使用构图。

```
function ArticleCardSkeleton(props) { ... }function ArticleCard(props) { ... }function **GridArticle**(props) {        **// 1**
  # Show a grid of articles
  return (
    <div class='article-grid'>
      **{props.children}               // 2**
    </div>
  );
}
```

现在，我将`ListArticle`重命名为`GridArticle` (1)组件，以更清楚地表明它是一个文章网格，并且我将权力授予`GridArticle`组件的用户，以定义哪些元素将通过`children` prop (2)呈现在网格内。

此时，您只有一个`GridArticle`组件可以在两种情况下使用。这意味着使用组件的用户定义了网格中包含的组件，而`GridArticle`只负责定义布局，我试图将这些组件视为组件布局。

```
// Grid of normal cards<GridArticle>
  <ArticleCard />
  <ArticleCard />
  <ArticleCard />
</GridArticle>// Grid of skeleton cards
<GridArticle>
  <ArticleCardSkeleton />
  <ArticleCardSkeleton />
  <ArticleCardSkeleton />
</GridArticle>
```

这并不是这个例子的全部，T2 还有一个额外的问题。您的第一个实现假设卡的页脚没有任何按钮，但是随着时间的推移，您需要添加一些额外的按钮，比如购物车或显示有优惠的消息。这是一个问题，你需要定义一个新的`ArticleCard`来复制相同的用户界面，但是添加这些可能的按钮和信息，或者更糟的是，你开始添加诸如`hasButton`、`message`、`offer`之类的道具，并有条件地渲染不同的部分。

所有这些都是不好的方法，但是构图概念和`children`道具在这种情况下可以帮助我们。

我们需要`ArticleCard`组件允许我们定义卡片的一些抽象部分，例如，卡片的“页脚”。按照上面的例子，我们可以使用`children`道具，并且可以传递任何组件，比如按钮、消息、链接等，作为卡片的“页脚”部分。

```
function ArticleCard(props) {
  return (
    <div>
      <div>props.article.name</div>
      <div>props.article.price</div>
      **{props.children}**
     </div>
  );
}
```

这是一个好的解决方案，但有时还不够。如果您想在卡片的“标题”部分留言，会发生什么？。`children`道具的主要优势在于，它是由 React 定义的道具，允许您以自然的方式指定内部组件(标签内的所有组件)，但是现在，您需要两个“区域”，所以，您需要定义另一个可以模拟第二个区域的道具，即“头部”区域。

```
function ArticleCard(props) {
  return (
    <div>
      **{props.header}**
      <div>props.article.name</div>
      <div>props.article.price</div>
      **{props.children}**
     </div>
  );
}
```

毕竟`children`道具只是一个标准道具，但是可以创建更多的道具来表示组件中的某个区域，在这种情况下，我们定义了一个`header`道具。我尽量使用最适合这种情况的通用术语，`header`只代表卡中的上级区域，通过分配一个通用术语，我保证正确的名称对于组件的未来使用来说是更清晰的，并且不仅仅是针对我目前的用例。

现在，您可以在许多情况下使用您的组件。

*   您只能定义`children`道具:

```
<ArticleCard>
  **<div class='footer-card'>
    I am the footer content
  </div>**
</ArticleCard>
```

*   您只能定义`header`道具。

```
<ArticleCard
  **header={
    <div class='header-card'>
      I am the header content
    </div>
  }**
/>
```

*   您可以定义两者。

```
<ArticleCard
  **header={
    <div class='header-card'>
      I am the header content
    </div>
  }**
>
  **<div class='footer-card'>
    I am the footer content
  </div>**
</ArticleCard>
```

如果您愿意，可以将`children`道具重命名为`footer`。这使得意义更加明显，唯一的问题是在使用时视觉上有点难看。

```
<ArticleCard
  **header={
    <div class='header-card'>
      I am the header content
    </div>
  }
  footer={
    <div class='footer-card'>
      I am the footer content
    </div>
  }** />
```

## 组合不仅仅是可重用的组件

构图不仅仅是 UI。组件的组合可以帮助您以更简洁的方式在应用程序的子组件中传播您的状态。

假设你有一个电子商务网站，你有一个购物车。购物车只是一个商品列表，用户保存这些商品以便在下一个时刻支付，但是你需要将这个状态传递给页面的许多部分，例如，导航栏(显示购物车中商品的计数器)，在`ArticleCard`中当用户点击商品时将商品添加到购物车，以及其他一些地方。目前，我们将注意力集中在期待购物车状态的`ArticleCard`组件上，我们将看看当我们不使用组合时会发生什么:

```
function NavBar() { ... }function ArticleList(props) {
  return props.articles.map((article) => <ArticleCard article={article} />);
}function ArticleCard(props) {
  return (
    <ArticleCardHeader article={props.article} />
    <ArticleCardBody article={props.article} />
    <ArticleCardFooter cart={props.cart}/>
  }
)function ArticleCardFooter(props) {
  return (
    <div>
      <div>...</div>
      <ShoppingCartButton article={props.article} cart={props.cart}
    </div>
  );
}**// The only component that requires the cart state
function ShoppingCartButton(props) {
  return <button onClick={() => cart.addItem(article)}>Add</button>;
}**function Page() {
  const cart = useCart();
  const articles = useArticles();return (
    <div>
      <NavBar cart={cart} />
      <ArticleList cart={t} articles={articles} />
    </div>
  );
}
```

如您所见，问题在于唯一需要知道购物车信息的组件是`ShoppingCartButton`，但是`ArticleList`、`ArticleCard`和`ArticleCardFooter`需要接收那个道具，唯一的目的是传递给`ShoppingCartButton`。

**注意。**这个问题一般称为[支柱钻孔](https://kentcdodds.com/blog/prop-drilling)。

这是一个更具层次性的问题模式:

```
Page  **(I have the shopping cart state!)**
  -- NavBar
  -- ArticleList
       -- ArticleCard
            -- ArticleCardHeader
            -- ArticleCardBody
            -- ArticleCardFooter
                 -- **ShoppingCartButton  (I need the shopping cart state!)**
```

我们没有在组件的内容中定义完整的实现，而是将其定义为一个组件布局，允许我们在`children` prop 中传递内容。结果是这样的:

```
function Page() {
  const cart = useCart();
  const articles = useArticles();return (
    <div>
      <NavBar cart={cart} />
      <ArticleList>
        <ArticleCard article={article}>
          <div>...</div>
 **<ShoppingCartButton article={article} cart={props.cart} />**
        </ArticleCard>
        ...
      </ArticleList>
    </div>
  );
}
```

如您所见，所有组件只接收它们真正需要的，唯一接收购物车状态的组件是`ShoppingCartButton`。

如果你对 React 有一点经验，你可能会考虑使用上下文。 [React Context](https://reactjs.org/docs/context.html) 允许你在你的 app 里放一个全局状态，并以一种快速的方式访问它，有什么问题？

*   **跟踪误差很困难。** React 上下文是一个**全局状态**。提供者内部的任何组件都可以访问它，并且根据情况的不同，任何组件都可以改变它的值，换句话说，跟踪问题是非常困难的。
*   **可重用组件较少。**您避免了 prop drilling 噪音，但是现在，您只能在自定义提供者内部使用您的组件，您不能在 de 提供者外部重用它们，因为他们需要访问他。
*   **来源歧义。**有时不清楚哪些信息是可用的或者信息来自哪里，与此相反，显式道具是传递所有信息的更显式的方式，并且确切地知道哪些信息是可用的以及它们的来源。

推荐你看[迈克尔杰克逊](https://www.youtube.com/watch?v=3XaXKiXtNjw)的视频。

## 作文并不总是正确的工具(个人观点)

合成并不总是正确的工具，React Context 是一种选择。

我个人的观点是在两种特殊情况下使用 React 上下文:

1.  当它是应用程序上的一个真正的全局状态时，比如身份验证状态。
2.  当你制造一些需要作为一个单元工作的组件组时，例如:

假设您定义了一个`Switch`和`Case`组件，它根据传递给`Switch`元素的值有条件地呈现一些元素。

该组件的预期用途是:

```
// ...
<Switch value={status}>
  <Case match='loading'>
    <p>Loading...</>
  </Case>
  <Case match='done'>
    <p>Done...</p>
  </Case>
  <Case match='error'>
    <p>Error...</p>
  </Case>
</Switch>
```

如您所见，所有组件作为一个整体工作。在`Switch`组件之外声明`Case`组件是没有意义的。

`Switch`组件将隐藏提供传递给它的值的提供者。所有的`Case`组件都将从中获取值，如果当前值与 case 值匹配，则决定呈现`children`属性。

**正确的粒度级别**

这种组合的一个副作用是可以看到包含每个组件的完整图片。如果用户界面很复杂，您可以得到如下结果:

```
const HomePage = () => {
  return (
    <Container>
      <Header>
        <Logo />
        <Menu>
          <MenuItem />
          <MenuItem />
          <MenuItem />
          <MenuItem />
        </Menu>
      </Header>

      <Body>
        <Controls>
         <SearchBar />
         <Filters>
           <Filter />
           <Filter />
           <Filter />
           <Filter />
         </Filters>
         <ArticleGrid>
           <Article>
             <ArticleLink/>
             <LikeButton/>
         </ArticleGrid>
         <PaginationControls />
      </Body>

      <Footer>
        <ContactInfo>
          <SocialNetwork />
          <SocialNetwork />
          <SocialNetwork />
        </ContactInfo>
        <Politicts />
      </Footer>
    </Container>
  );
}
```

当您定义组件的状态和完整实现时，这可能更糟，但问题是这是`HomePage`组件。在大多数情况下，当你进入一个页面组件时，你只需要改变页面的某个特定部分，你不一定需要看到页面每个部分的完整实现。

当我遇到一些具有高级组件的情况时，我更喜欢创建单独的组件来定义页面的高级部分，并在这些组件中的每一个上委托合成:

```
const Header = () => {
  return (
      <HeaderContainer>
        <Logo />
        <Menu>
          <MenuItem />
          <MenuItem />
          <MenuItem />
          <MenuItem />
        </Menu>
      </HeaderContainer>
  );
}const Body = () => {
  return (
      <Body>
        <Controls>
         <SearchBar />
         <Filters>
           <Filter />
           <Filter />
           <Filter />
           <Filter />
         </Filters>
         <ArticleGrid>
           <Article>
             <ArticleLink/>
             <LikeButton/>
         </ArticleGrid>
         <PaginationControls />
      </Body>
  );
}const Footer = () => {
  return (
      <Footer>
        <ContactInfo>
          <SocialNetwork />
          <SocialNetwork />
          <SocialNetwork />
        </ContactInfo>
        <Politicts />
      </Footer>
    </Container>
  );
}const HomePage = () => {
  return (
    <Container>
      <Header />
      <Body />
      <Footer />
    </Container>
  );
}
```

这有许多优点:

*   根据组件的抽象级别，您只显示必要的细节。
*   如果您像第一个实现一样向应用程序添加一个状态，那么每次状态改变时，您都要重新呈现所有的页面组件，如果该状态只对页面的一部分是必需的，则是独立的。

## 结论

*   作文不仅仅是一个反应的概念。可以用函数，类等做作文。
*   儿童道具是制作组件组合的良好资源。
*   组合允许您定义可重用的组件。
*   组件的组成可以改善你的状态流。
*   合成的一种替代方法是使用带有 React 上下文的全局状态。
*   更喜欢作文而不是反应上下文。
*   使用复合时，要注意抽象的粒度级别。
*   道具演练并不总是不好的，有时候构图并不是合适的工具。

## 参考

*   [反应成分](https://www.youtube.com/watch?v=3XaXKiXtNjw)
*   [支柱钻孔](https://kentcdodds.com/blog/prop-drilling)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*