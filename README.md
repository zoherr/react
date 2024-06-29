# React

## Start Project

`npm create vite@latest`


## Tailwind

`https://tailwindcss.com/docs/guides/vite`

# # 
# 

# Syllabus
- Hooks
- React Router
- Context API

# 
# 
# 
# React Concept

### Understanding React’s Virtual DOM, Fiber, and Reconciliation

- https://medium.com/@zohaibshahzad16/understanding-reacts-virtual-dom-fiber-and-reconciliation-ed6b07187728



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
