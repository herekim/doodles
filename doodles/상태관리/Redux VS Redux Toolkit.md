Redux Toolkit은 Redux 코드에서 여러 번 반복되는 부분을 줄여주고, 코드를 더 간결하게 만들어줍니다. 액션 타입과 액션 생성자를 별도로 만들 필요 없이 `createSlice`를 사용해서 한 번에 만들 수 있습니다. 또한 `configureStore`를 사용해서 Redux 개발자 도구와 미들웨어를 쉽게 설정할 수 있습니다.
## Redux
먼저 Redux를 사용해서 만드는 경우입니다.
### actions/counterActions.js
```js
export const INCREMENT = "INCREMENT"; 
export const DECREMENT = "DECREMENT";  
export const increment = () => ({ type: INCREMENT });  
export const decrement = () => ({ type: DECREMENT });
```
### reducers/counterReducer.js
```js
import { INCREMENT, DECREMENT } from "../actions/counterActions";  
const initialState = { count: 0 };  
const counterReducer = (state = initialState, action) => {
	switch (action.type) {     
		case INCREMENT:       
			return { count: state.count + 1 };     
		case DECREMENT:      
			return { count: state.count - 1 };     
		default:       
			return state;   
	}};  

export default counterReducer;
```
### store.js
```js
import { createStore } from "redux";
import counterReducer from "./reducers/counterReducer";

const store = createStore(counterReducer);

export default store;

```
## Redux Toolkit
이제 Redux Toolkit을 사용해서 만드는 경우입니다.
### slice.js
```js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { count: 0 },
  reducers: {
    increment: (state) => {
      state.count += 1;
    },
    decrement: (state) => {
      state.count -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;

export default counterSlice.reducer;

```
### store.js
```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./slice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});

```