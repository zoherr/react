# React

## Start Project

`npm create vite@latest`


## Tailwind

`https://tailwindcss.com/docs/guides/vite`

# # 
# 

# Syllabus
- Hooks
- Cutom Hooks
- React Router
- Context API
- Redux - Toolkit

# 
# 
# 
# React Concept

### Understanding React’s Virtual DOM, Fiber, and Reconciliation

- https://medium.com/@zohaibshahzad16/understanding-reacts-virtual-dom-fiber-and-reconciliation-ed6b07187728


#
# Hooks


## 1. State Hooks
   - `useState`: Allows you to add state to functional components.
   - Example:
     ```jsx
     import React, { useState } from 'react';

     function Counter() {
       const [count, setCount] = useState(0);

       return (
         <div>
           <p>You clicked {count} times</p>
           <button onClick={() => setCount(count + 1)}>Click me</button>
         </div>
       );
     }
     ```

## 2. Effect Hooks
   - `useEffect`: Allows you to perform side effects in functional components (e.g., data fetching, subscriptions).
   - Example:
     ```jsx
     import React, { useState, useEffect } from 'react';

     function Example() {
       const [count, setCount] = useState(0);

       useEffect(() => {
         document.title = `You clicked ${count} times`;
       }, [count]); // Only re-run the effect if count changes

       return (
         <div>
           <p>You clicked {count} times</p>
           <button onClick={() => setCount(count + 1)}>Click me</button>
         </div>
       );
     }
     ```

## 3. Context Hooks
   - `useContext`: Allows you to use context to share values between components without passing props.
   - Example:
     ```jsx
     import React, { useContext } from 'react';

     const MyContext = React.createContext();

     function Component() {
       const value = useContext(MyContext);
       return <div>{value}</div>;
     }

     function App() {
       return (
         <MyContext.Provider value="Hello, world!">
           <Component />
         </MyContext.Provider>
       );
     }
     ```

## 4. Ref Hooks
   - `useRef`: Allows you to create a mutable object that persists across re-renders, often used for accessing DOM elements directly.
   - Example:
     ```jsx
     import React, { useRef } from 'react';

     function FocusInput() {
       const inputRef = useRef(null);

       const focusInput = () => {
         inputRef.current.focus();
       };

       return (
         <div>
           <input ref={inputRef} type="text" />
           <button onClick={focusInput}>Focus the input</button>
         </div>
       );
     }
     ```

## 5. Memoization Hooks
   - `useMemo`: Memoizes a computed value to optimize performance.
   - Example:
     ```jsx
     import React, { useMemo } from 'react';

     function ExpensiveCalculationComponent({ input }) {
       const result = useMemo(() => {
         // Perform an expensive calculation here
         return input  2;
       }, [input]);

       return <div>Result: {result}</div>;
     }
     ```

   - `useCallback`: Memoizes a callback function to optimize performance.
   - Example:
     ```jsx
     import React, { useState, useCallback } from 'react';

     function Button({ onClick }) {
       return <button onClick={onClick}>Click me</button>;
     }

     function App() {
       const [count, setCount] = useState(0);

       const handleClick = useCallback(() => {
         setCount(count + 1);
       }, [count]);

       return (
         <div>
           <p>You clicked {count} times</p>
           <Button onClick={handleClick} />
         </div>
       );
     }
     ```


# 
# Custom Hooks
- custom hooks are JavaScript functions that allow you to reuse stateful logic between different components. They are a way to extract and share common logic without repeating code. Custom hooks follow the same rules as React hooks, and their names typically start with "use" to differentiate them from regular functions.

### Creating a Custom Hook

A custom hook is essentially a function that uses built-in React hooks and returns some state or behavior. Here's a basic example:

#### Example: Custom Hook for Fetching Data

```jsx
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

### Using the Custom Hook

You can use the custom hook `useFetch` in any functional component:

```jsx
import React from 'react';
import useFetch from './useFetch'; // Import the custom hook

function App() {
  const { data, loading, error } = useFetch('https://api.example.com/data');

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <div>
      <h1>Data:</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default App;
```

### Key Concept

- **State and Effect Hooks**: Custom hooks can use `useState`, `useEffect`, and other React hooks internally.
- **Parameterization**: Custom hooks can take parameters to make them more flexible.
- **Return Values**: Custom hooks can return any type of value (e.g., objects, arrays) that the consuming component needs.


# # 
# 

# React Router

`npm install react-router-dom`

# 

### Router Documentations 
```
https://reactrouter.com/en/main/start/overview
```

# 

## Router Features

- NavLink
`https://reactrouter.com/en/main/components/nav-link`
- Link
`https://reactrouter.com/en/main/components/link`
- loader
`https://reactrouter.com/en/main/start/overview#data-loading`
# 
- if you use Outlet(App.jsx) that let you use to do nesting - Means if you want to Fix your header and footer just want to change inside things
`https://reactrouter.com/en/main/components/outlet`
# 

## Router Implementation

### Main.jsx 

```javascript
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App />}>
      <Route path="" element={<Hero />} />
      <Route path="about" element={<AboutUs />} />
      <Route path='user/:userid' element={<User />} />
    </Route>
  )
);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);


```


### app.jsx

```javascript

import { Outlet } from 'react-router-dom'
import Header from './components/Header/Header'
import Footer from './components/Footer/Footer'

function App() {
  return (
    <>
    <Header/>
    <Outlet/>
    <Footer/>
    </>
  )
}

export default App;

```
# 
## 
## When you get Data from params (/user/id)
### user.jsx

```javascript
import React from 'react'
import { useParams } from 'react-router-dom'

function User() {
    const {userid} = useParams()
  return (
    <div className='bg-gray-600 text-white text-3xl p-4'>User: {userid}</div>
  )
}

export default User
```
# # 
# 
# Context Api

### The Context API in React is a way to share values (such as data or functions) between components without having to pass props down manually at every level. It provides a way to effectively manage state and propagate it throughout your component tree.
#
## When to Use Context
### Context is primarily used when you need to share data that can be considered "global" for a tree of React components. Typical use cases include:

- Theme settings (light/dark mode)
- User authentication status and details

## App.jsx

``` javascript 
  <UserProvider>
        <User  />
   </UserProvider>
 ```

## Steps (2 Methods)

### 1st Method (Without Creating Hook)
for this Method we create Different Files
- Creating a Context
```javascript
import React from 'react'
const UserContext = React.createContext()
export default UserContext;

```
- Providing the Context
``` javascript
import React from "react";
import UserContext from "./UserContext";
const UserContextProvider = ({children}) => {
    const [user, setUser] = React.useState(null)
    return(
        <UserContext.Provider value={{user, setUser}}>
        {children}
        </UserContext.Provider>
    )
}
export default UserContextProvider
```
- Consuming the Context
```javascript
import { UserContext } from './UserContext';

const { user, setUser, logout } = useContext(UserContext);
```


# 
### 2st Method (With Creating Hook)
for this Method we create Only one File
- Creating a Context,Providing the Context,Creating Hook
```javascript
// 1
// Create the context 
import { createContext, useContext, useState } from "react";
export const UserContext = createContext();

// 2
// Create a provider component
export const UserProvider = ({ children }) => {
    const [user, setUser] = useState(null);
    const logout = () => {
        setUser(null);
    };

    return (
         <UserContext.Provider value={{ user, setUser, logout }}>
             {children}
         </UserContext.Provider>
    );
};

// 3
// Custom hook to use the UserContext
 export default function useUser() {
     return useContext(UserContext);
}
```
- Consuming the Context
```javascript
 const { user, setUser, logout } = useUser();
```
# 

### 3rd Method
```javascript
import {createContext, useContext} from "react"

export const TodoContext = createContext({
    todos: [
        {
            id: 1,
            todo: " Todo msg",
            completed: false,
        }
    ],
    addTodo: (todo) => {},
    updateTodo: (id, todo) => {},
    deleteTodo: (id) => {},
    toggleComplete: (id) => {}
})


export const useTodo = () => {
    return useContext(TodoContext)
}

export const TodoProvider = TodoContext.Provider
```
# 
# 
# Redux-Toolkit

### 1. What is Redux Toolkit?

Redux Toolkit is the official, recommended way to write Redux logic. It simplifies configuring the store, reduces boilerplate code, and includes good defaults for common use cases.

### 2. Key Concepts in Redux Toolkit

- Store: The place where the entire state of your application is stored.
- State: The data or information your application uses.
- Action: An object that describes a change you want to make to the state.
- Reducer: A function that takes the current state and an action, then returns the new state.
- Slice: A collection of Redux reducer logic and actions for a single feature of your app.

### 3. Setting Up Redux Toolkit

First, let's set up a simple React application and install Redux Toolkit.

```bash
npm install @reduxjs/toolkit react-redux
```

### 4. Creating a Slice

A slice contains the logic for a specific feature of your app. For example, let's create a counter slice.

src/features/counter/counterSlice.js

```javascript
import { createSlice } from '@reduxjs/toolkit';

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

### 5. Configuring the Store

Next, configure the store to use the counter slice reducer.

src/app/store.js

```javascript
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

### 6. Setting Up the Provider

Wrap your application with the Redux Provider and pass the store to it.

src/index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { Provider } from 'react-redux';
import { store } from './app/store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

### 7. Using the Redux State and Actions in Components

Now you can use the Redux state and actions in your components using hooks provided by React-Redux.

src/App.js

```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, incrementByAmount } from './features/counter/counterSlice';

function App() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div className="App">
      <header className="App-header">
        <h1>Counter: {count}</h1>
        <button onClick={() => dispatch(increment())}>Increment</button>
        <button onClick={() => dispatch(decrement())}>Decrement</button>
        <button onClick={() => dispatch(incrementByAmount(5))}>Increment by 5</button>
      </header>
    </div>
  );
}

export default App;
```

### Summary

1. Install Redux Toolkit and React-Redux.
2. Create a slice with `createSlice`.
3. Configure the store with `configureStore`.
4. Wrap your app with the `Provider` and pass the store.
5. Use Redux state and actions in your components with `useSelector` and `useDispatch`.

