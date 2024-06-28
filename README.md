# React

## Start Project

`npm create vite@latest`


## Tailwind

`https://tailwindcss.com/docs/guides/vite`
# 
# 

# Syllabus
- Hooks
- React Router

# 
# 
# React Concept

### Understanding React’s Virtual DOM, Fiber, and Reconciliation

- https://medium.com/@zohaibshahzad16/understanding-reacts-virtual-dom-fiber-and-reconciliation-ed6b07187728



# 
# 

# React Router

`npm install react-router-dom`

# 

### Router Documentations 
```
https://reactrouter.com/en/main/start/overview
```
- After 55:00
  `https://www.youtube.com/watch?v=VJov5QWEKE4&t=885s`
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
