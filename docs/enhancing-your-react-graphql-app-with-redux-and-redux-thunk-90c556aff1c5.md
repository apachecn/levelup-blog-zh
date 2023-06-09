# 使用 Redux 和 Redux-Thunk 增强您的 React + GraphQL 应用程序

> 原文：<https://levelup.gitconnected.com/enhancing-your-react-graphql-app-with-redux-and-redux-thunk-90c556aff1c5>

继续 React + GraphQL 全栈教程，应用 Redux 方法和中间件

![](img/b1bc7557288906bbde0f47b5a9168ff0.png)

# 回到过去

在我的[之前的故事](/using-graphql-api-with-node-js-and-react-forms-8b13f4b26361)中，我们用 React JS 单页应用程序(SPA)创建了一个 GraphQL API 作为前端。在那篇教程中，我们避免了现实世界应用程序的一些复杂性，以使事情尽可能简单。在该教程中，每次页面加载时，用户搜索表单都是空白的。为了解决这个问题，我们将使用临时存储来存储搜索参数。

我们还将为后面的故事保存用户验证。在这个故事中不考虑它，因为这个主题值得一个完全独立的文章。

最后，我们在上一篇教程中使用了[容器](https://github.com/KilroggD/GraphQL-react/tree/master/client/src/containers)方法，其中一些组件是管理自身状态的容器，并且还执行所有副作用，比如 AJAX API 调用。这种方法适用于相对较小的应用程序，但是当应用程序增长时，将状态和动作一起保存在组件中就变得不那么方便了。

找出状态的哪个片段和哪个动作位于哪个组件中并不总是一个简单的问题。此外，随着时间的推移，包含组件代码的 JavaScript 文件变得越来越大，可读性越来越差。为了解决这个问题，我们需要从容器中提取状态，并使全局应用程序状态成为“真实的单一来源”基于状态的操作动作，以及所有副作用，如 API 调用或存储使用，也应该从组件代码中抽象出来。

为了解决这个问题，我建议使用流行的、众所周知的状态管理方法和名为 [Redux](https://redux.js.org/) 的库。您可以在这个新的库中找到、克隆和启动工作代码，这个库是为后端带有 GraphQL 的 Redux-enhanced 应用程序创建的。

# 为什么是 Redux？

有许多用于数据流和状态管理的工具——那么为什么是 Redux 呢？

![](img/3c22603a543293e24ed755b5ba14c2ed.png)

*   著名的 JS 应用程序状态管理容器，有一个大的社区和积极的支持。
*   非常适合 React JS 应用程序。
*   允许您拥有一个全局状态存储作为“真实的单一来源”
*   保持状态树独立于 UI 和表示组件。
*   状态的某些部分可以映射到应用程序的特定部分。
*   提供处理动作和副作用(API 调用等)的灵活性。).

上面最后一点值得特别注意。根据 [Redux concepts](https://redux.js.org/docs/introduction/CoreConcepts.html) 的说法，reducer 是一个[纯函数](https://en.wikipedia.org/wiki/Pure_function)，它管理你的 app 状态的一个片段(接受一个初始状态和动作作为参数，并返回一个新状态)。

```
const formReducer = (state = initialState, action) => {
    switch (action.type) {
        case 'FORM_LOAD':
            return {
                ...state,
                data: action.data,
            }
        default:
            return state
    }
}
```

因此，不应该在 reducers 中使用诸如 API 调用或存储操作之类的副作用。但是如果我们需要它们，该怎么办呢？比如异步加载用户/待办事项列表？为了这个目的，[中间件](https://redux.js.org/docs/advanced/Middleware.html) connect 存在了。

# 中间件和异步操作

中间件对于异步操作和 API 调用非常有用。您可以使用中间件来处理从 AJAX 请求开始到检索数据的所有管道。让我们看一个小例子——我们需要请求一个后端 API 为我们提供一个用户列表，但是当 API 调用正在进行时，我们希望将我们的应用程序置于“正在加载”状态，如果我们在调度数据时出现任何错误，则置于“错误”状态。

这种模式被称为中间件。它接受你的参数并返回一个新的函数，这个函数实现所有需要的副作用并分派你的实际动作，随后影响你的 reducers 和你的应用程序的状态。我们还能够使用 async/await 模式来处理承诺和 AJAX 调用。

使用 redux-thunk 中间件，它将看起来像。

```
const getUsers = (params) => async dispatch => {
    try {
        dispatch(requestUsers())
        const data = await ApiService.getUsers(params)
        dispatch(receiveUsers(data))
    } catch(e) {
        dispatch(failureUsers())
    }
}
```

创建异步操作后，我们将通过调度 requestUsers()操作将容器置于加载状态。它将等待从服务器检索数据，然后，要么通过调用 receiveUsers()操作用用户列表更新我们的状态，要么通过调度 failureUsers()操作将其置于错误状态。

这个中间件有更多的“超能力”，比如通过 getState 函数访问应用程序的当前状态。这个故事后面会讲。

所有的动作都是触发 reducers 的简单函数。

```
const requestUsers = () => ({
    type: 'USERS_REQUEST'
})const receiveUsers = (data) => ({
    type: 'USERS_RECEIVE',
    data
})const failureUsers = () => ({
    type: 'USERS_FAILURE',
}) 
```

# 重新思考容器

![](img/45b0e6f4d9adb0d725346f908f210a50.png)

正如我们在前面的故事中看到的，容器是“智能”组件，它处理自己的状态并触发动作和副作用，如 API 调用，存储状态中接收的数据并将其作为道具传递给子组件。

对于我们重构的应用程序，我们需要以一种冗余的方式重新思考容器。Redux 中的容器是连接到全局状态存储的“无状态”组件。Redux 让我们能够映射我们需要的状态片段和我们想要传递给容器道具的动作。代替*状态*，容器的*属性*被更新。Redux 的核心原则之一是通过存储和 reducers 处理整个应用程序状态。

下面的例子展示了我们的 [TodosListContainer](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/containers/TodoListContainer.js) 。我们通过 reducers 管理状态，并通过 mapStateToProps 将特定的状态片段映射到组件的 Props，通过 mapDispatchToProps 函数将特定的动作映射到 props。我们通过从“react-redux”模块导入的 connect()函数将这些函数应用于我们的容器。

我们在组件挂载上调度 loadTodos 来检索 Todos 列表。我们还有特定的条件来处理来自与“Todo”部分相关的状态位的加载和错误标志。

```
import React from 'react'
import TodoList from '../components/TodoList'
import { Link } from 'react-router-dom'
import { connect } from 'react-redux'
import { todosAction } from '../actions/todosActions'class TodoListContainer extends React.Component { componentDidMount() {
        const userId = parseInt(this.props.match.params.userId, 10);
        //load todos here
        this.props.loadTodos(userId)
    } render() {//add loading and failure state
        if (this.props.isLoading) {
            return <span>Loading...</span>
        } if (this.props.isFailure) {
            return <span>Error loading todos!</span>
        } return (
            <div className="todo">
                <TodoList todos={this.props.todos} />
                <Link className="todo__linkback" to='/'>
                     Back to Users search
                </Link>
            </div>
        );
    }}const mapStateToProps = ({ todos }) => {
    return {
        ...todos
    }
}const mapDispatchToProps = (dispatch) => {
    return {
        loadTodos: (userId) => {
            dispatch(todosAction({ userId }))
        }
    }
}export default connect(
    mapStateToProps, mapDispatchToProps
)(TodoListContainer);
```

# 冗余路由器

[Redux router](https://github.com/reactjs/react-router-redux) 或 react-router-redux 是一个增强的 React 路由器，它允许您将 React 路由器与您的 Redux 商店协调，并将与路由相关的一段状态与您的商店同步。它还为您提供了一个非常有用的 push()函数，允许您以函数的方式在 Redux 操作中执行重定向。

在本教程中，我们将不会使用 Redux 路由器的主要功能，但它有利于我们应用程序的未来改进(即认证)。如果你不想安装和使用它，在本教程中使用通用的 React-router 也可以。

# 将存储用于搜索表单

为了保持不同路径之间的表单数据同步，我们需要一些存储空间，既可以现在存放表单数据，也可以以后从中检索。对于本教程，我们将选择[本地存储](https://www.w3schools.com/html/html5_webstorage.asp)。这有几个原因:

*   本地存储数据没有生存期，它会一直存在，直到我们删除它。
*   本地存储不需要任何额外的库或工具——一切都可以通过 HTML5 localStorage API 来完成。

为了从实际的存储引擎中抽象出来——以便我们可以切换到会话存储或 cookies，并遵循更好的常规做法——我们创建了一个 StorageService 来处理本地存储数据。

该类包含对实际存储引擎的引用以及获取/设置/删除值的有用方法。我们将在 redux 中间件中调用它来填充搜索表单数据。

我们将在成功的搜索请求之后用数据填充这个存储——这将在本教程的后面描述。

```
class StorageService {
    constructor() {
        this.storage = window.localStorage
        this.form_key = 'search_form'
    }getSearchData() {
        let data = this.storage.getItem(this.form_key) || false;
        if (data) {
            return JSON.parse(data)
        }
    }setSearchData(data) {
        if (data) {
            this.storage.setItem(
                this.form_key, JSON.stringify(data)
            );
        }
    }removeSearchData() {
        this.storage.removeItem(this.form_key);
    }}export default new StorageService()
```

# 用 redux 处理表单

在之前的教程中，我们控制了 [UserForm](https://github.com/KilroggD/GraphQL-react/blob/master/client/src/forms/UserForm.js) 组件，它有自己的状态，所有的输入变化都映射到其中。为了让这个表单以 Redux 友好的方式工作，我们需要为它创建一个 reducer 和 actions。还有令人敬畏的 [Redux-Form](https://redux-form.com) 库，它给你很多“开箱即用”的功能，但这可能是另一个故事的一部分。:)

先说行动。我们定义了从 localStorage 加载表单数据的操作，如果其中一个输入发生了变化，就改变表单数据，并清除表单数据，因为我们将从这里开始存储成功的搜索请求，所以需要一个清除方法。

```
import StorageService from '../StorageService'const loadForm = (data) => ({
    type: 'FORM_LOAD',
    data,
})const clearForm = () => ({
    type: 'FORM_CLEAR',
})export const loadFormAction = () => (dispatch) => {
    //load form data from local storage
    const data = StorageService.getSearchData() || {}
    //dispatch an action
    dispatch(loadForm(data))
}export const clearFormAction = () => (dispatch) => {
    StorageService.removeSearchData()
    dispatch(clearForm())
}
```

表单的缩减器看起来非常简单——只需要 loadForm 从用户输入或本地存储中加载表单数据，clearForm 清除数据。

```
const formReducer = (state = {}, action) => {
    switch (action.type) {
        case 'FORM_LOAD':
            return {
                ...state,
                ...action.data,
            }
        case 'FORM_CLEAR':
            return {}
        default:
            return state
    }
}export default formReducer
```

您可以看到[用户表单](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/forms/UserForm.js)组件是如何重写的，以及处理程序和道具是如何从[用户容器](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/containers/UserListContainer.js)组件传递到那里的。

# 总结—在我们的应用中重复主要概念

要安装所有讨论过的依赖项，只需运行:

```
npm i -s redux react-redux redux-thunk
npm i -s react-router-redux@next //if you want to use redux-router
```

或者使用可以使用[资源库](https://github.com/KilroggD/GraphQL-react-redux)中的 package.json 文件。

为了使用全局状态的所有 reducers，我们将使用 Redux 中的 combineReducers 函数。它允许我们将每个 reducer 的状态片段与适当的别名结合起来。参见/reducers 中的 [index.js](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/reducers/index.js) 文件。

```
const reducer = combineReducers(
    {
        form: formReducer,
        todos: todosReducer,
        users: usersReducer,
        routerReducer
    }
)export default reducer
```

在此之后，我们的状态对象将看起来像:

```
state = {
    form: {}, //form reducer part
    users: {}, //users reducer part
    todos: {}, //todos reducer part
    routerReducer: {}, //react-router-redux part
}
```

现在让我们转到主 [index.js](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/index.js) 文件:

```
const history = createHistory()
const middleware = [thunk, routerMiddleware(history)]const store = createStore(
    reducer,
    applyMiddleware(...middleware)
);ReactDOM.render(
    <Provider store={store}>
        <ConnectedRouter history={history}>
            <App />
        </ConnectedRouter>
    </Provider>,
    document.getElementById('root'));
registerServiceWorker();
```

前两行创建所有需要的中间件——thunk 用于中间件，async actions 和 routerMiddleware 用于处理历史和路由。

之后，我们只需用前面提到的组合缩减器初始化存储，并将应用程序包装在 Provider 中，并将存储传递给它。

以 [UsersListContainer](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/containers/UserListContainer.js) 为例，让我们看看 Redux 容器是如何工作的:

```
import React from 'react'
import UserList from '../components/UserList'
import UserForm from '../forms/UserForm'
import { connect } from 'react-redux'
import { getUsers } from '../actions/usersActions'
import { loadForm, loadFormAction, clearFormAction } from '../actions/formActions'class UserListContainer extends React.Component { componentDidMount() {
        this.props.loadForm();
        this.props.search();
    } render() {
        //add loading and failure state
        if (this.props.isLoading) {
            return <span>Loading...</span>
        } if (this.props.isFailure) {
            return <span>Error loading users!</span>
        } return <div className="user">
            <UserForm data={this.props.form}
                submitHandler={this.props.search}
                changeHandler={this.props.changeForm}
                clearHandler={this.props.clearForm} />
            {this.props.users && 
               <UserList users={this.props.users} />}
          </div>;
    }
}const mapStateToProps = ({ users, form }) => {
    return {
        ...users,
        form,
    }
}const mapDispatchToProps = (dispatch) => {
    return {
        search: () => { dispatch(getUsers()) },
        loadForm: () => { dispatch(loadFormAction()) },
        changeForm: (params) => { dispatch(loadForm(params)) },
        clearForm: (params) => {
            dispatch(clearFormAction())
            dispatch(getUsers())
         },
    }
}export default connect(mapStateToProps, mapDispatchToProps)(UserListContainer);
```

在这个容器中，我们将状态的“用户”和“表单”部分映射到容器的属性。我们还通过 mapDispatchToProps 函数映射我们需要的所有动作。当组件挂载时，我们从存储中加载表单数据，并使用当前参数执行用户搜索。我们还将一些动作作为处理程序传递给 UserForm。

[Users Reducer](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/reducers/usersReducer.js) 管理我们状态中与用户相关的部分，并处理请求/接收/失败动作类型:

```
const initialState = {
    isLoading: false,
    isFailure: false,
    users: null,
}const usersReducer = (state = initialState, action) => {
    switch (action.type) {
        case 'USERS_REQUEST':
            return {
                ...state,
                isLoading: true,
                isFailure: false,
            }
        case 'USERS_RECEIVE':
            return {
                ...state,
                isLoading: false,
                isFailure: false,
                users: action.data,
            }
        case 'USERS_FAILURE':
            return {
                ...state,
                isLoading: false,
                isFailure: true,
            }
        default:
            return state
    }
}export default usersReducer
```

[用户动作](https://github.com/KilroggD/GraphQL-react-redux/blob/master/client/src/actions/usersActions.js)文件包含一个中间件函数，它调度所有这些动作，执行异步 API 调用，并在请求成功时存储表单数据。注意，在本教程中，我们在中间件函数中使用了 getState 功能。这个函数为您提供了对当前状态的访问，因此您可以获取表单数据或其他状态位，而不必将它们传递给操作。

```
import ApiService from '../ApiService'
import StorageService from '../StorageService'const requestUsers = () => ({
    type: 'USERS_REQUEST',
})const receiveUsers = (data) => ({
    type: 'USERS_RECEIVE',
    data,
})const failureUsers = () => ({
    type: 'USERS_FAILURE',
})export const getUsers = (params) => async (dispatch, getState) => {
    try {
        dispatch(requestUsers())
        const params = getState().form
        const data = await ApiService.getUsers(params)
        if (Object.keys(params).length && data) {
            //save successful request
            StorageService.setSearchData(params)
        }
        dispatch(receiveUsers(data))
    } catch (e) {
        dispatch(failureUsers())
    }
}
```

结果，我们现在有了 SPA，状态完全由 Redux 管理。我们有两个“智能”容器(TodosList 和 UsersList ),我们没有改变表示组件(除了在 UserForm 组件中进行了一点重构，这不仅仅是为了表示)。表单数据现在可以在路线更改之间保存:例如，我们可以搜索一个用户，查看 todos，然后返回到列表，它仍然会被过滤！随意克隆回购并测试代码:)

在我接下来的故事中，我们将讨论在 GraphQL 和 React-Redux 中处理认证，以及 React-Redux 应用程序的单元测试。

![](img/966fe76453a92e24f4f726e9cd2ece21.png)