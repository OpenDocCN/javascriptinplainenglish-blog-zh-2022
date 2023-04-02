# 如何测试 React 组件

> 原文：<https://javascript.plainenglish.io/how-to-test-react-components-2eff11d8cd75?source=collection_archive---------3----------------------->

![](img/1213a040c95fcec5b2260cdd6ae5cf94.png)

编写测试 React 组件的测试可能很棘手。我花时间寻找做这件事的正确方法，但我几乎找不到解决问题所需的例子。这让我想写这篇文章来分享我的经验和见解。

# 设置环境

如果你想知道如何设置 Jest 和 React 测试库环境，你也可以阅读这篇文章。

# 演示存储库

如果你想看一个完整的例子，我创建了一个样板用于演示:【https://github.com/tabsteveyang/react-jest-rtl-boilerplate

# 嘲弄的

在设置了运行 Jest 和 React 测试库的环境之后，您可能很快就会发现，当您在测试中渲染它时，您的一些组件会崩溃。

这是因为测试中呈现的组件只能在特定的环境下运行。它通常已经在开发和生产环境中设置好了，但是我们必须在运行测试时模拟一个假的。

我将把本节中创建的文件放在 jest/mock/目录下，并在 webpack.config.js 文件中添加一个@jest 别名。

```
alias: {
  '@js': path.resolve(__dirname, 'src/js/'),
  '@scss': path.resolve(__dirname, 'src/scss/'),
  '@img': path.resolve(__dirname, 'img/'),
  '@jest': path.resolve(__dirname, 'jest/')
}
```

并将它添加到 jest.config.js 中

```
moduleNameMapper: {
  '^@js(.*)$': '<rootDir>/src/js$1',
  '^@scss(.*)$': '<rootDir>/src/scss$1',
  '^@img(.*)$': '<rootDir>/img$1',
  '^@jest(.*)$': '<rootDir>/jest$1'
},
```

## 嘲讽 Redux

1.创建实际商店的副本

在某些情况下，我们只需要一个可以用默认状态呈现组件的环境。您可以通过复制实际的故事文件并删除不必要的配置(比如 Redux DevTools 的配置)来实现这一点

```
// jest/mock/store/index.jsimport { createStore, applyMiddleware, compose } from 'redux'
import thunk from 'redux-thunk'
import reducer from '@js/reducers'const composeEnhancers = composeconst middleware = [thunk]
export default createStore(
  reducer,
  composeEnhancers(applyMiddleware(...middleware))
)
```

2.模仿提供者

如果我们使用 React with Redux，我们需要将组件包装到 react-redux 库中的提供者组件中。我们需要在测试中渲染组件时做同样的事情。为了避免重复编写相同的逻辑，我们可以创建一个组件来处理它。

```
// jest/mock/MockProvider.jsximport { Provider } from 'react-redux'
// use the replica one as the default store
import store from './store'const MockProvider = ({ children = null, mockStore = null }) => {
  return (
    <Provider store={mockStore || store}>
      { children }
    </Provider>
  )
}MockProvider.propTypes = {
  mockStore: PropTypes.object,  // this prop allows us to set the store to specific state
  children: PropTypes.node
}export default MockProvider
```

我们还必须创建一个模块来创建商店的不同状态。该模块使用 redux-mock-store 库创建模拟存储，并用 Jest 模拟函数替换模拟存储的 dispatch 属性，以便我们可以在需要时跟踪状态。我们可以用这个参数来设置存储的初始状态。

```
// jest/mock/store/createMockStore.jsimport configureMockStore from 'redux-mock-store'
import thunk from 'redux-thunk'
const middleware = [thunk]
export default (initialState) => {
  const mockStore = configureMockStore(middleware)(initialState)
  // eslint-disable-next-line no-undef
  // replace the dispatch method with a spy and keep the funtionality
  mockStore.dispatch = jest.fn(mockStore.dispatch)
  return mockStore
}
```

## 嘲讽路线和历史

这里还有一个类似的案例。为了使使用 react-router-dom 库的组件工作，我们必须将它们包装在路由器组件中。因此，我们也可以为此创建一个模块。

```
// jest/mock/mockRouter.jsximport { Router } from 'react-router-dom'
import { createBrowserHistory } from 'history'const MockRouter = ({ children }) => {
  return (
    <Router history={createBrowserHistory()}>
      { children }
    </Router>
  )
}MockRouter.propTypes = {
  children: PropTypes.node  // prop for sending in the components that you want to render
}export default MockRouter
```

## 模拟导入模块

在某些情况下，有必要在测试中模拟模块(包括来自 npm 的包),下面是这样做的一个例子:

```
import { render, cleanup } from '@testing-library/react'
import MainPage from '../MainPage'// *** must write it in the global scope ***
// mock the react-router-dom library
// and replace the useHistory attribute of the module
jest.mock('react-router-dom', () => ({
  useHistory: () => ({
    push: jest.fn()
  })
}))afterEach(cleanup)
beforeEach(() => {
  // ...
})describe('MainPage.jsx', () => {
  // ...
}
```

你可以在[官方文档](https://jestjs.io/docs/mock-functions)中阅读更多关于模拟函数的内容，稍后你会看到更多的例子。

# 考什么？

react-testing-library 的创建者(Kent C. Dodds)创建了一个工具来帮助开发人员避免测试[实现细节](https://kentcdodds.com/blog/testing-implementation-details)，这样我们就不会在试图重构组件时忙于修复测试用例。

这意味着您应该专注于测试组件如何与用户交互。编写测试时，假设用户正在使用组件，并测试组件是否反应正常。因此，了解如何做到以下几点至关重要:

**1。模仿用户**

我们可以使用[@ testing-library/user-event](https://testing-library.com/docs/ecosystem-user-event/)库来模拟一个用户。对于用户事件不能实现的事件，使用@testing-library/react 库中的 fireEvent。

**2。查询 DOM**

*   来自屏幕对象的查询

使用 render 方法呈现组件后，可以使用 screen 对象访问结果，并使用它进行查询。你可以在官方的[备忘单](https://testing-library.com/docs/react-testing-library/cheatsheet/)中读到更多相关信息。(有一张顺手的桌子！)

*   按类名查询

screen 对象没有提供按类名查询的方法，但还是有办法做到的；您可以使用容器属性获取根 DOM，然后调用 getElementsByClassName 方法:

```
import { render } from '@testing-library/react'it('some description', () => {
  const screen = render(<Component />)
  screen.container.getElementsByClassName('<the_target_class_name>')
}
```

# 情节

**1。一个简单的组件**

*   根据道具渲染

如果你要测试的组件仅仅因为它们的属性不同而不同，你要做的就是编写向组件发送不同属性的测试并检查。

为了使它更简单，在一般情况下，我将只编写测试用例:

a.所有具有真实价值的道具

b.所有有虚假价值的道具

并使用 react-test-renderer 库对这些场景进行快照测试，以节省测试这些细节的查询时间。

```
import { cleanup } from '@testing-library/react'
import renderer from 'react-test-renderer'  // renderer for snapshot test
import UserInfo from '../UserInfo'afterEach(cleanup)describe('UserInfo.jsx', () => {
  it('snapshot renders correctly, truthy values', () => {
    const tree = renderer
      .create(<UserInfo
          userId="202200001"
          userName="Test User"
          userImg="./test_user.img"
        />)
      .toJSON()
    expect(tree).toMatchSnapshot()
  })
  it('snapshot renders correctly, falsy values', () => {
    const tree = renderer
      .create(<UserInfo/>)
      .toJSON()
    expect(tree).toMatchSnapshot()
  })
})
```

*   根据缩减器渲染

测试因减速器状态而异的组件与最后一种情况非常相似。您可以将 reducers 的状态模拟成特定的值，并呈现组件。然后，同样，您可以通过执行一些查询或快照测试来检查结果。

```
import { cleanup } from '@testing-library/react'
import renderer from 'react-test-renderer'
import MockProvider from '@jest/mock/MockProvider'
import createMockStore from '@jest/mock/store/createMockStore'
import UserInfoV2 from '../UserInfoV2'afterEach(cleanup)describe('UserInfoV2.jsx', () => {
  it('snapshot renders correctly, truthy values', () => {
    const store = createMockStore({
      userInfo: {
        userId: '202200001',
        userName: 'Test User',
        userImg: './test_user.img'
      }
    })
    const tree = renderer
      .create(<MockProvider mockStore={store}>
        <UserInfoV2 />
      </MockProvider>)
      .toJSON()
    expect(tree).toMatchSnapshot()
  })
  it('snapshot renders correctly, falsy values', () => {
    const store = createMockStore({
      userInfo: {
        userId: '',
        userName: '',
        userImg: ''
      }
    })
    const tree = renderer
      .create(<MockProvider mockStore={store}>
        <UserInfoV2 />
      </MockProvider>)
      .toJSON()
    expect(tree).toMatchSnapshot()
  })
})
```

**2。具有间隔和承诺的组件**

如果有什么事情需要等待一段时间才能完成，您应该尝试 waitFor 和 findBy 查询。你可以很容易地在网上找到例子，所以我将跳过细节。

**3。带挂钩的组件**

正如在模仿部分提到的，我们可以使用 jest 来模仿所有导入的模块。钩子也是一样的！

*   SPA 路由参数

例如，假设有一个使用 react-router-dom 库中的 useParams 钩子的数据页面组件:

```
import { useParams } from 'react-router-dom'const DataPage = (props) => {
  const { dataId = '' } = useParams()
  const data = {
    data1: 'this is the content form data 1',
    data2: 'this is the content form data 2',
  }
  return (
    <div className="data-page">
      { 
        data[dataId]
          ? <div className="data-page__content">{data[dataId]}</div>
          : <div className="data-page__not-found">content not found</div>
      }
    </div>
  )
}export default DataPage
```

这里有一种模拟 useParams 将返回的值的方法:

```
import { screen, render, cleanup } from '@testing-library/react'
import DataPage from '../DataPage'afterEach(cleanup)jest.mock('react-router-dom', () => ({
  ...jest.requireActual('react-router-dom'),
  useParams: () => ({
    dataId: 'data1'
  })
}))describe('DataPage.jsx', () => {
  it('render the content if data exist', () => {
    render(<DataPage />)
    screen.getByText('this is the content form data 1')
  })
})
```

*   自定义挂钩返回数组中的函数

假设有这样一个组件:

```
import { useSearchData } from '@js/hooks/searchData'const SearchPage = (props) => {
  const [search] = useSearchData() // the custom hook
  const onSearchButtonClick = () => {
    search()
  }return (
    <div className="search-page">
      <button onClick={onSearchButtonClick}>search</button>
    </div>
  )
}export default SearchPage
```

您可以用这种方式模仿自定义挂钩:

```
import { screen, render, cleanup } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import SearchPage from '../SearchPage'
import { useSearchData } from '@js/hooks/searchData'afterEach(cleanup)jest.mock('@js/hooks/searchData', () => {
  const spy = jest.fn()
  return {
    useSearchData: () => {
      return [spy]
    }
  }
})describe('SearchPage.jsx', () => {
  it('render the content if data exist', () => {
    render(<SearchPage />)
    // initialize the imported function,
    // and get the reference of the spy
    const [search] = useSearchData()
    userEvent.click(screen.getByText('search'))
    expect(search).toHaveBeenCalled()
  })
})
```

**4。带有导入模块的组件**

让我们更深入地研究测试数据页面组件的情况。在前面的例子中，我们只能模拟一次 useParams 的实现。

如果希望保持可操作性，可以先模拟整个模块，在呈现组件之前使用 mockImplementationOnce 或 mockReturnValueOnce 方法。通过这样做，您可以为每个测试用例模拟函数的实现或返回值。

此外，如果组件中的代码依赖于函数的结果，模仿函数的实现可以让我们避免错误。

```
import { screen, render, cleanup } from '[@testing](http://twitter.com/testing)-library/react'
import { useParams } from 'react-router-dom'
import DataPage from '../DataPage'afterEach(cleanup)jest.mock('react-router-dom', () => {
  const spy = jest.fn()
  return {
    ...jest.requireActual('react-router-dom'),
    useParams: spy
  }
})describe('DataPage.jsx', () => {
  it('render the content if data exist', () => {
    useParams.mockImplementationOnce(() => ({
      dataId: 'data1'
    }))
    render(<DataPage />)
    screen.getByText('this is the content form data 1')
  })
  it('render the hint if data does not exist', () => {
    useParams.mockReturnValueOnce({
      dataId: ''
    })
    render(<DataPage />)
    screen.getByText('content not found')
  })
})
```

通常，您可以模仿整个库并继续:

```
jest.mock('react-router-dom')
```

但是如果我们模仿整个 react-router-dom 库，由于某种原因，useParams 属性将变得未定义，所以我使用上一个例子中的方法。

**5。分派动作的组件**

尽管指南告诉我们要避免测试实现细节，但我仍然认为测试组件分派的动作是必要的。我关心的事情是:

*   **时机:**是否在正确的时间以正确的行动调度火灾？
*   **参数:**发送给动作的参数是否正确？

实际上，您还可以测试那些导入的函数(包括导入的模块、动作和库)的计时和参数

这可能是一个奇怪的例子，但我试图在一个组件中涵盖更广泛的场景:

```
import { useEffect } from 'react'
import { useDispatch, useSelector } from 'react-redux'
import {
  setSettings,  // a plain object action
  startGetSettings  // a redux-thunk action
} from '@js/actions'const DemoPage = (props) => {
  const dispatch = useDispatch()
  const { title = '' } = useSelector(state => state.settings) useEffect(() => {
    dispatch(setSettings({
      title: 'Title set when the component mount.'
    }))
  }, []) const onFetchClick = () => {
    dispatch(startGetSettings({ foo: 'bar' }))
  } return (
    <div className="demo-page">
      <h1>{title}</h1>
      <button onClick={onFetchClick}>fetch settings</button>
    </div>
  )
}export default DemoPage
```

如果我们测试一个返回普通对象的动作，这是非常简单的:

```
it('should dispatch setSettings action when the component mount', () => {
  const mockStore = createMockStore({
    settings: {}
  })
  render(<MockProvider mockStore={mockStore}>
    <DemoPage />
  </MockProvider>)
  // the Nth element from the result of the getActions method
  // will be the object sent by Nth dispatch.
  expect(mockStore.getActions()[0].type).toBe(actions.SET_SETTINGS)
  expect(mockStore.getActions()[0].data.title).toBe('Title set when the component mount.')
  expect(mockStore.dispatch).toHaveBeenCalledTimes(1)
})
```

另一方面，如果你正在测试一个 redux-thunk 动作，这将是非常难以管理的。因为动作应该返回一个对象，所以如果你把返回值当作一个承诺，就会导致一个错误。

因此，我决定把这些动作模仿成一般的动作:

```
jest.mock('@js/actions', () => ({
  // keep the functionality of the action module
  ...jest.requireActual('@js/actions'),
  // replace the thunk-action into a plain object action,
  // to test the received parameters.
  startGetSettings: parameters => ({ type: 'MOCK', parameters })
}))
```

并用 getActions 方法的结果验证时间和参数:

```
it('should dispatch startGetSettings action when user click the button', async () => {
  const mockStore = createMockStore({
    settings: {}
  })
  render(<MockProvider mockStore={mockStore}>
    <DemoPage />
  </MockProvider>)
  userEvent.click(screen.getByText('fetch settings'))
  await waitFor(() => {
    expect(mockStore.getActions()[1].parameters)
      .toEqual({ foo: 'bar' })
    expect(mockStore.dispatch).toHaveBeenCalledTimes(2)
  })
})
```

这里的关键点是定义边界。如果您正在为一个组件编写测试，那么您应该关注该组件中的逻辑。测试那些导入函数的时间和参数就足够了。最好创建相关的测试文件来测试这些部分的细节。

# 结局

我想每个人都有自己编写测试的方式，这就是我实现自己的方式。欢迎在评论中留下你的想法，这样我们都能成为更好的开发者🤓

# 阅读更多关于单元测试的内容

*   [为单元测试建立 Jest 和 React 测试库](https://medium.com/@tabsteveyang/setup-jest-and-react-testing-library-for-unit-testing-9be43df32fd5)

# 参考

1.  [https://jestjs.io/docs/mock-functions](https://jestjs.io/docs/mock-functions)
2.  [https://kentcdodds.com/blog/testing-implementation-details](https://kentcdodds.com/blog/testing-implementation-details)
3.  https://testing-library.com/docs/ecosystem-user-event/
4.  [https://testing-library . com/docs/react-testing-library/cheat sheet/](https://testing-library.com/docs/react-testing-library/cheatsheet/)
5.  [https://www . codecademy . com/learn/learn-react-testing/modules/react-testing-library/cheat sheet](https://www.codecademy.com/learn/learn-react-testing/modules/react-testing-library/cheatsheet)

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***