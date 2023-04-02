# 停止过度复杂的网络开发——尝试精简

> 原文：<https://javascript.plainenglish.io/stop-overcomplicating-web-development-try-svelte-a188ca2a79fa?source=collection_archive---------8----------------------->

## 展示苗条身材的核心特征。

![](img/8395e65ed09f2f768b466db8f22d84ea.png)

Svelte 被评为 2021 年最受开发者喜爱的 web 框架[(链接)](https://insights.stackoverflow.com/survey/2021#section-most-loved-dreaded-and-wanted-web-frameworks)。那么什么是苗条，为什么如此受人喜爱呢？

Svelte 是一个相当独特的 javascript 框架，它的目标是“真正的反应性”并帮助开发者“编写更少的代码”。

它有一个很棒的特性，通过让框架本身在编译阶段“消失”来创建微小的代码包，发布优化的普通 JavaScript 代码，而不是使用运行时加载的大型复杂的库。

在我看来，这是让 Svelte 从其他 JavaScript 框架中脱颖而出的游戏规则改变者。一个小的包意味着更快的加载时间，这似乎是网络发展的方向，因为越来越多的数据显示了快速网站的好处。这个编译阶段还消除了对 React 和 Vue.js 使用的虚拟 DOM 等技术的需求，进一步提高了网站的速度。

另一个特点是没有样板文件。Svelte 感觉非常接近标准的 web 开发，其中组件看起来完全像普通的 HTML。我相信这是开发者喜欢这个框架的一个重要原因。

为了介绍 Svelte，让我们使用 [PokeAPI](https://pokeapi.co/) 创建一个简单的单页应用程序，用户可以在其中选择一个口袋妖怪，并带有一个实时搜索栏来过滤所有口袋妖怪的列表。这将以一种有用的方式展示苗条身材的所有核心特征。完整的代码可以在[这里](https://github.com/EB1811/svelte-searcher-tut)找到。

# 装置

先装基本的 Svelte 吧。为此，请运行以下命令:

```
npx degit sveltejs/template new-svelte-project
```

这将把简单的模板复制到你想要的文件夹中。要启用 TypeScript，进入新的 svelte 文件夹，运行:

```
node scripts/setupTypeScript.js
```

现在您需要做的就是通过运行以下命令来安装必要的文件

```
npm install
```

# 组件特征

一个苗条的组件是一个以. svelte.
结尾的文件，正如你在 App.svelte 中看到的，一个苗条的组件可以非常简单，包含三个部分；HTML，一个放置 javascript 的脚本标签和一个放置 CSS 的样式标签。这类似于 Vue，只是没有样板代码。

清除 App.svelte 的脚本和 HTML 内容，让我们在 style 标签中使用给定的 CSS。

# 变量和反应性

变量是在脚本标签中创建的。通过使用花括号{}，我们可以非常容易地创建一个字符串变量并在 DOM 中显示它。

```
<! — For example →
<script lang=”ts”>
 let name: string = ‘pokemon searcher’
</script><h1>{name}</h1>
```

为了搜索口袋妖怪的名字，我们需要一个输入字段和一个保存该字段内容的变量。
为了使‘口袋妖怪名称’变量等于输入字段的内容，我们可以使用一个特殊的细长关键字‘bind’，它允许‘口袋妖怪名称’变量的双向绑定。

```
<!-- App.svelte -->
<script lang="ts">
  let pokemonName: string = ''
</script><main>
  <span>Search: </span>
  <input type="text" bind:value="{pokemonName}" /><h1>Pokemon: {pokemonName}</h1>
</main>
```

现在，在输入字段中输入内容会改变口袋妖怪标题的输出。
该 bind 关键字支持双向绑定，而无需像 React 中那样使用“onInput”函数来更改“pokemonName”变量的值。

# onMount & Async 获取

对于这个示例应用程序，我们将 PokeAPI 中的 pokemon 名称作为字符串数组存储在一个变量中。

我们希望组件一呈现出来就获取数据并进行映射。
为此，我们可以使用‘on mount’，这是一个简单的生命周期函数，在组件第一次呈现到 DOM 后运行。让我们用它从 PokeAPI 中获取数据，并将其映射到一个口袋妖怪名称数组中。

```
<!-- App.svelte - script tag -->
<script lang="ts">
  import { onMount } from 'svelte' let pokemonName: string = '' // Fetch from api then store the mapped names.
  let pokemonData: string[] = []
  onMount(() => {
    const setPokemonData = async (): Promise<void> => {
      const rawPokemonData = await (
        await fetch('[https://pokeapi.co/api/v2/pokemon?limit=99'](https://pokeapi.co/api/v2/pokemon?limit=99'))
      ).json() pokemonData = rawPokemonData.results.map(
        (p: { name: string; url: string }) => p.name
      )
    }
    setPokemonData()
  })
</script>
```

我们现在在“pokemonData”数组中有一个 Pokemon 名称列表，我们可以在我们的简单项目中使用它。

# 被动声明

对于 live search 特性，我们需要一个数组来保存用户从 Pokemon 名称中输入的内容。

Svelte 有一个很棒的工具来处理从其他属性派生的状态，即反应性声明。它们看起来像这样。

```
$: reactiveVar = otherVar * 2;
```

现在，“reactiveVar”是一个变量，但是每当“otherVar”变量发生变化时，都会计算它的值(当计算中使用的变量发生变化时，svelte 会运行计算)。

我们可以将保存过滤后的口袋妖怪名称的变量变成一个反应性声明。我们称这些为“建议”。

```
<!-- App.svelte - bottom of script tag -->
<script>
  // ...

  let suggestions: string[]
  $: suggestions = 
       pokemonName.length > 0
         ? pokemonData.filter(
             (name) => name.includes(pokemonName)
           )
         : pokemonData
</script>
```

因此，“suggestions”是一个口袋妖怪名称数组，其中包含输入字段中输入的字符串。

被动赋值不能与 typescript 一起使用，所以我们可以声明一个“建议”变量来保留类型检查。

# 环

我们希望在页面上显示这个“建议”数组的内容，我们可以通过使用一个细长的循环来实现。Svelte 有一个特殊的关键字“each ”,使我们能够显示给定 iterable 中每一项的 DOM 元素。
要显示每个口袋妖怪的名字，只需使用每个关键字循环“口袋妖怪数据”变量。

```
<!-- App.svelte - html -->
<main>
  <span>Search: </span>
  <input type="text" bind:value="{pokemonName}" />

  {#each suggestions as suggestion}
    <h2>{suggestion}</h2>
  {/each}
</main>
```

当我们在输入字段中键入内容时，我们可以看到建议列表发生了变化。对于这样简单的代码来说很酷。

# 条件渲染

Svelte 还有其他关键词。另一个有用的是`#if`。`#if`关键字允许条件逻辑。

例如，当我们从 PokeAPI 获取数据时，我们可以呈现一个加载屏幕。

```
<!-- App.svelte - html -->
<main>
  {#if pokemonData && pokemonData.length > 0}
    <span>Search: </span>
    <input type="text" bind:value="{pokemonName}" />

    {#each suggestions as suggestion}
      <h2>{suggestion}</h2>
    {/each}
  {:else}
    <h2>Loading...</h2>
  {/if}
</main>
```

# 组件和道具

Props 用于将数据从一个组件传递到另一个组件。这对于框架来说是相当标准的，并且语法非常简单。

为了表示一个组件接受一个属性，export 关键字被用于一个变量。

```
<script lang="ts">
  export let stringProp: string
</script>
```

现在，要传递“stringProp”的值，只需在编写组件时使用导出变量的名称。

```
<script lang="ts">
  import NewComponent from './NewComponent.svelte'
</script>

<NewComponent  stringProp="prop value"  />
```

对于我们的应用程序，让我们为每个建议创建一个组件。

在 src/

```
<!-- Suggestion.svelte -->
<script lang="ts">
  export let suggestion: string
</script>

<div class="suggestion">{suggestion}</div>

<style>
    .suggestion {
        font-size: 1.25rem;
    }
</style>
```

现在，我们可以导入这个组件并在我们的#每个循环中使用它。

```
<!-- App.svelte - top of script tag -->
<script lang="ts">
  import Suggestion from './Suggestion.svelte'

  // ...
  // ...
</script><!-- App.svelte - html -->
<main>
  {#if pokemonData && pokemonData.length > 0}
    <span>Search: </span>
    <input type="text" bind:value="{pokemonName}" />

    {#each suggestions as suggestion}
      <Suggestion suggestion="{suggestion}"/>
    {/each}
  {:else}
    <h2>Loading...</h2>
  {/if}
</main>
```

这在目前是毫无意义的，所以让我们以事件的形式为“建议”部分添加一些逻辑。

# 自定义事件

自定义事件可以从一个组件分派到另一个组件。这使我们能够进行亲子沟通。

对于我们的应用，我们希望能够点击一个建议来选择我们的口袋妖怪。我们可以通过将一个自定义事件从“建议”组件发送到应用程序组件，然后设置一个变量的值来保存我们选择的口袋妖怪。

首先，创建新的“chosenPokemon”变量，并在 App.svelte 的屏幕上显示。

```
<!-- App.svelte - bottom of script tag -->
<script lang="ts">
  // ...
  // ...

  let chosenPokemon: string = ''
</script><!-- App.svelte - html -->
<main>
  {#if pokemonData && pokemonData.length > 0}
    <h1>Chose Your Pokemon</h1>
    <h2>Chosen Pokemon: {chosenPokemon}</h2>

    <div>
      <span>Search: </span>
      <input type="text" bind:value="{pokemonName}" />

      {#each suggestions as suggestion}
        <Suggestion suggestion="{suggestion}"/>
      {/each}
    </div>
  {:else}
    <h2>Loading...</h2>
  {/if}
</main>
```

现在，在建议中，我们可以在点击建议时发送一个定制的“chosePokemon”事件。

为了创建一个自定义事件，我们需要从 svelte 导入“createEventDispatcher”。

```
<!-- Suggestion.svelte - script tag -->
<script lang="ts">
  import { createEventDispatcher } from 'svelte'

  export let suggestion: string

  // Function to dispatch a custom event.
  const dispatch = createEventDispatcher()
  const chosePokemon = (): void => {
    dispatch('chosePokemon', {
      pokemon: suggestion
    })
  }
</script>
```

我们现在有一个“chosePokemon”函数，它将一个自定义的“chosePokemon”事件分派给父组件。

要在点击建议时调用该函数，我们需要使用像这样的“点击”事件。

```
<!-- Suggestion.svelte - html -->
<div class="suggestion" on:click="{chosePokemon}">
  {suggestion}
</div>
```

回到 App.svelte 文件，我们可以通过使用“on:(事件名称)”语法来处理这个自定义事件。

```
<!-- App.svelte - 'Suggestion' component in html -->
<Suggestion
  suggestion="{suggestion}"
  on:chosePokemon="{(e) => {
    chosenPokemon = e.detail.pokemon
  }}"
/>
```

此处理程序将 chosenPokemon 变量的值设置为等于自定义事件中传递的 Pokemon 名称(位于“detail”属性中)。当我们点击一个建议时，那个口袋妖怪的名字就会显示出来。

我已经通过这种方式设置了“chosenPokemon”变量来引入自定义事件，但是，还有一种更干净、更简单的方法:绑定转发。

# 绑定转发

我们看到了在创建输入字段时如何使用 bind 关键字来设置双向绑定，但是这个关键字也可以在我们的组件中使用。

在 App.svelte 中，我们可以用 chosenPokemon 道具上的 bind 关键字替换 chosePokemon 事件处理程序。

```
<!-- App.svelte - 'Suggestion' component in html -->
<Suggestion suggestion="{suggestion}" bind:chosenPokemon />
```

在“建议”组件中，我们可以接受这个道具，使“点击”功能简单地设置这个“chosenPokemon”变量。

```
<!-- Suggestion.svelte -->
<script lang="ts">
  export let suggestion: string
  export let chosenPokemon: string = ''
</script>

<div 
  class="suggestion" 
  on:click="{() => chosenPokemon = suggestion}"
>
  {suggestion}
</div>
```

我们现在使用一小部分代码就拥有了和以前一样的功能。

# 商店

我想通过介绍商店来总结一下。

有了 Svelte，我们不需要使用像 Redux 这样的外部库来拥有一个中央存储，它是与框架一起出现的。

从根本上说，存储是一个具有 subscribe 方法的对象，该方法允许我们的 Svelte 组件被告知存储值的任何变化。Svelte 定义了两种不同类型的存储，一种是可写存储，一种是可读存储。顾名思义，可写存储允许读取和写入，而可读存储只允许读取。

对于我们的应用程序，我们将把“口袋妖怪数据”变量发送到商店。由于这个变量只是收集和存储口袋妖怪数据，我们将使用可读的存储。

首先，我们需要 src 文件夹中的一个新文件(我将它命名为“stores.ts”)。
我们可以从 svelte 导入可读存储函数，以及所需的类型。

```
// stores.ts
import { readable, Readable, Subscriber } from 'svelte/store'
```

一个可读的函数，作为它的第一个参数，接受存储的初始值，作为它的第二个参数，一个“开始”函数。这个“start”函数在商店获得第一个订阅者时被调用，所以它是我们检索 API 数据的地方。

该函数接收一个“set”回调函数，该函数用于设置存储的值，并返回一个“stop”函数，该函数在最后一个订户取消订阅时被调用(在这里我们可以执行一些清理)。

在我们的商店中，我们可以简单地复制我们的' setPokemonData '函数的内容，但我们不是分配' PokemonData '的值，而是调用' set '函数。

```
import { readable, Readable, Subscriber } from 'svelte/store'

const setPokemonData = 
  async (set: Subscriber<string[]>): Promise<void> => {
    const rawPokemonData = await (
      await fetch('https://pokeapi.co/api/v2/pokemon?limit=99')
    ).json()

    set(
      rawPokemonData.results.map(
        (p: { name: string; url: string }) => p.name
      )
    )
  }

// Export the new store 'pokemonData' variable.
export const pokemonData: Readable<string[]> = 
  readable([], (set) => {
    setPokemonData(set)

    return () => set([])
  })
```

就是这样。我们现在有一个中央商店，在“口袋妖怪数据”中保存我们的口袋妖怪名称。

要使用我们的商店，我们需要从我们的商店文件导入' pokemonData '变量。然后，我们可以使用特殊的细长“$”符号来引用商店的价值。

```
<!-- App.svelte -->
<script lang="ts">
  import { pokemonData } from './stores.js'
  import Suggestion from './Suggestion.svelte'

  let pokemonName: string = ''

  let suggestions: string[]
  // $pokemonData instead of pokemonData
  $: suggestions =
    pokemonName.length > 0
      ? $pokemonData.filter((name) => 
          name.includes(pokemonName)
        )
      : $pokemonData

  let chosenPokemon: string = ''
</script>

<main>
  {#if $pokemonData && $pokemonData.length > 0}
    <h1>Chose Your Pokemon</h1>
    <h2>Chosen Pokemon: {chosenPokemon}</h2>

    <div>
      <span>Search: </span>
      <input type="text" bind:value="{pokemonName}" />
      {#each suggestions as suggestion}
        <Suggestion 
          suggestion="{suggestion}" 
          bind:chosenPokemon 
        />
      {/each}
    </div>
  {:else}
    <h2>Loading...</h2>
  {/if}
</main>
```

我们的应用程序工作原理相同，但是我们的 API 数据现在集中存储，可以在任何组件中使用。

现在，虽然 svelte 有可写和可读的存储，但任何坚持 svelte 存储“契约”并实现 subscribe 方法的东西都是存储。这意味着商店非常灵活，可以根据您的需求量身定制。你甚至可以用另一种语言创建一个商店，比如 Rust，如下图所示。

# 最终注释

Svelte 在混乱的 JavaScript 框架世界中脱颖而出，因为它没有为了开发者体验而牺牲用户体验，反之亦然。

Svelte 提供了神奇的工具，使开发应用程序变得容易，而它的编译器为最终用户带来了一个微小的软件包，大大减少了下载时间。

Svelte 成为最受欢迎的框架已经有一段时间了，尽管它的使用越来越多，这是它将变得像 Vue 或 React 一样大的潜在迹象。这与最近对更高性能 web 的推动不谋而合，从提供给客户端的疯狂的大型 JavaScript 包转向服务器端或混合呈现。

Svelte 团队现在正在开发 SvelteKit，这是 Svelte 的 Next.js 版本，你可以在这里了解:

[](https://kit.svelte.dev/) [## 苗条套装

### SvelteKit 是官方的 Svelte 应用程序框架

kit.svelte.dev](https://kit.svelte.dev/) 

如果你喜欢这篇文章，请考虑分享它。

看看我的 [GitHub](https://github.com/EB1811) 和其他[文章](https://dev.to/emmanuilsb)。

*原载于 2022 年 3 月 20 日*[*https://dev . to*](https://dev.to/emmanuilsb/stop-overcomplicating-web-development-try-svelte-47ln)*。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*