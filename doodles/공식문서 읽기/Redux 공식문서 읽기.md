# 소개
## Redux 시작하기
1. [[Redux]]의 장점은 일관적인 동작 보장, 테스트하기 쉬운 앱, 상태의 중앙화된 관리, 쉬운 디버깅, 어떤 UI 레이어에서도 동작 등이 있다.
2. Redux는 공식적으로 Redux Toolkit(RTK)의 사용을 권장한다. RTK는 Redux 사용에 필요한 패키지를 포함하고 있으며, 스토어 생성, 리듀서의 생성과 불변성을 보장하는 업데이트, slice 등을 포함하고 있어 더욱 심플하고 안정적인 전역 상태 관리를 제공할 수 있다.
3. React에서 Redux를 설치하는 권장하는 방법은 `Vite with our Redux+TS Template`을 사용하는 방법과, `Next's with-redux Template`을 사용하는 것이 있다.
4. Redux는 단 하나의 스토어를 가지고 있다. 상태를 변경하는 유일한 방법은 Action을 만들어서 스토어로 dispatch하는 것이다. Action에 대해 스토어가 어떻게 바뀌는지 구체적으로 명시하는 것은 Reducer 함수에서 담당한다. 스토어 값은 객체, 배열, 기본형 데이터 타입만 포함한다. Reducer는 이전 스토어 값을 토대로 계산을 하며, 항상 새로운 값을 반환해야 한다.
5. 보통 Reducer에서는 Action에 따른 조건문을 작성하는데, switch 문을 사용하는 것이 일반적이다.
6. Redux를 선택해야 하는지는 상황에 따라 다르다. 1) 앱이 커지면서 데이터 변경이 자주, 다양한 곳에서 일어나는 경우 2) 상태 변화에 대한 단일한 스토어가 필요한 경우 3) Props Drilling 문제에서 벗어나고 싶은 경우가 있을 수 있다.
## Redux Toolkit을 추천하는 이유
### Redux에 대한 이해와 Redux가 가진 문제
- Redux는 전역 상태를 포함하는 단일 스토어, 사용자의 행동이 일어나면 해당 행동(액션)을 스토어에 전달(디스패치), 액션을 기반으로 불변성을 유지한 상태로 업데이트된 상태를 반환해서 스토어를 변경하는 순수한 리듀서 함수를 가진다.
- 이 밖에도 보통 Redux 코드에는 액션 생성자, 미들웨어, Thunk 함수, Redux DevTools 등의 다양한 항목들이 포함된다.
- Redux 코어는 의도적으로 매우 작고 사용자의 선택의 여지가 많도록 작성된 라이브러리다. createStore를 통해 스토어를 생성하고, combineReducers로 여러 slice 리듀서를 하나의 큰 리듀서로 결합하고, applyMiddleware로 여러 개의 미들웨어를 스토어 enhancer로 결합하고, compose로 여러 개의 스토어 enhancer를 하나로 결합한다. 이 밖에도 모든 로직은 사용자가 직접 작성해야 한다.
- 이렇게 '직접 작성'해야 하는 부분이 많다는 부분이 바로 Redux Toolkit이 탄생한 이유다. 리듀서 함수는 그저 함수다. Pure Redux는 switch문을 통해 액션의 타입에 따라 새로운 상태를 반환한다. 간단한 코드를 위해 액션 생성자, 액션 타입, 리듀서 등 여러 파일에 긴 코드를 작성해야 하고, 이는 결국 실수를 유발하는 확률을 높이게 된다.
### Redux Toolkit는 어떻게 이 문제를 해결하는가
- Redux Toolkit은 Pure Redux의 다양한 보일러 플레이트를 제거하고, 보다 간단한 API를 제공해서 사용자의 실수를 줄일 수 있다. 대표적으로 configureStore, createSlice API가 있다.
- configureStore는 한 번의 호출로 Redux 스토어를 설정한다. 이 곳에서 리듀서를 결합하고, 미들웨어를 추가하고, DevTools를 통합할 수 있다.
- createSlice는 액션 생성자 함수를 자동으로 생성하고, 리듀서 이름에 기반해 내부적으로 액션 타입 문자열을 생성한다. 또한 내부에서는 Immer 라이브러리를 사용하고 있어서, Mutating 하게 상태를 변경해도 불변성을 지켜준다.
- 결국 Pure Redux에서 액션 타입 문자열을 만들고, 액션 생성자 함수를 만들고, 해당 액션 생성자 함수에 따른 리듀서를 만드는 과정이 createSlice 함수 하나에 포함된 것이다. 
- 이 밖에도 비동기 액션 전후에 액션을 디스패치하는 createAsyncThunk 등 Redux 작업을 수행할 수 있는 다양한 API를 제공한다. [자세히](https://ko.redux.js.org/introduction/why-rtk-is-redux-today/#redux-toolkit%EC%9D%80-%EB%AC%B4%EC%96%BC-%ED%95%98%EB%82%98%EC%9A%94)
- 데이터 패칭과 캐싱을 지원하는 RTK Query가 있다. `const { data, isFetching} = useGetPokemonQuery('pikachu')`과 같은 형태로 사용할 수 있다.
### 기존 Redux 패턴이 보일러 플레이트가 많고 복잡했던 몇 가지 이유
- 최초의 Flux 아키텍처가 일부 같은 접근 방식을 사용했다.
	- Flux 아키텍처는 페이스북 개발팀에서 제안한 상태 관리 아키텍처. MVC의 복잡성을 해결하기 위해 도입. 데이터 흐름의 단방향성이 핵심 개념. Dispatcher, Stores, Views, Actions로 이루어져 있다.
	- Redux는 이 Flux 아키텍처를 발전시켜 상태 관리를 단순화했다. 결국 Redux가 Flux 아키텍처를 기반으로 만들어졌고, Flux 아키텍처의 일부 접근 방식을 사용한 것이다.
		- Redux에는 Dispatcher의 개념이 스토어의 메서드인 dispatch에 내장되어 있다. 하지만 이는 Flux 아키텍처의 Dispatcher 개념을 축소해 
- 초기 Redux 문서에서 코드를 타입별로 다른 파일에 분리하도록 액션 타입 상수 예시를 제시했다.
- JS가 기본적으로 가변 언어이기 때문에 불변 업데이트를 위해선 수동 객체 복사가 필요했다.
- Redux는 몇 주 안에 만들어졌고, 의도적으로 기본적인 API만 지원하도록 설계되었다.
- 부수효과를 작성하는 일반 접근 방법으로 redux-saga 미들웨어 사용을 강조했다.
- 액션 객체에 대한 TS 타입을 수작업으로 작성하고, 유니언 타입을 생성하여 타입 수준에서 디스패치할 수 있는 액션을 제한하도록 강조했다.
## 핵심 컨셉
## 학습 리소스
# 튜토리얼
