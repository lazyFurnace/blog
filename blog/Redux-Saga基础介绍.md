# redux-saga

## 基本用法

```js
// Store.js
import { createStore, applyMiddleware } from "redux";
import createSagaMiddleware from "redux-saga";
import { rootSaga } from "./Sagas";

const sagaMiddleware = createSagaMiddleware();
const store = createStore(reducer, applyMiddleware(sagaMiddleware));
sagaMiddleware.run(rootSaga);
```

```js
// Saga.js
export function* rootSaga() {
  yield ...
  yield ...
}
```

## 常用 API

### put

触发一个 action。

```js
yield put({ type: "SOME_ACRION", payload });
```

### call

调用一个函数，如果这个函数返回一个 promise ，那么它会阻塞 saga，直到promise成功被处理。

```js
yield call(api);
```

### fork

执行一个非阻塞操作。

```js
yield fork(someThing);
```

### select

从 redux 中获取数据

```js
yield select(state => state.someState);
```

### take

暂停并等待 action 触发。

```js
yield take("SOME_ACTION");
```

### takeLatest

接收执行所触发的 action，然后返回最后一次调用的结果。如果我们多次触发，它只关注最后一个返回的结果。

```js
yield takeLatest("SOME_ACTION", handleFun),
```

### takeEvery

接收执行所触发的 action

```js
yield takeEvery("SOME_ACTION", handleFun),
```

## 相关文章

[处理异步利器 -- Redux-saga](https://www.zcfy.cc/article/async-operations-using-redux-saga-freecodecamp-2377.html)

[Demo 地址](https://github.com/andresmijares/async-redux-saga)

