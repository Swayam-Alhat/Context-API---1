# Context API in React js.

we are going to learn and understand the Context API.
<br/>
The context API is use to avoid the Prop drilling issue. there are lots of data which we have to pass in various components. this we can do with passing prop. but as the project grows it became very complicated because we are passing data in such components that dont need the data.
\*\* So To directly
<br>

## A simple four step trick 🌟

1. Create a context (Box).
2. Create a provider.
3. Then use it with needy components.
4. Wrap the whole App or components by Provider.

## Exaplanation

First see the files and folder so that you will get the idea of project.
**Imagine the context API like Global storage where data is stored which is going to use in various components.Even in nested components.**
<br/>

## First step

Make a file in under components folder. name the file UserContext or GlobalContext. in this project there is file name "UserContext.js".

the file contains the follwing the code.

```javascript
import React from "react";
const UserContext = React.createContext();
export default UserContext;
```

imagine we build a box ( _means the context where data is going to stored_ ) and box name is UserContext. this box is created using the hook createContext();
<br/>
Through this box the data is going to send to perticular component.

## Second step

Making a another file which is named as Provider. In this case, the file name is "ContextProvider.jsx".

<hr>
This file contains the following code.

```javascript
import React, { useState } from "react";
import UserContext from "./UserContext";

const ContextProvider = ({ children }) => {
  const [userData, setUserData] = useState("");
  return (
    <UserContext.Provider value={{ userData, setUserData }}>
      {children}
    </UserContext.Provider>
  );
};

export default ContextProvider;
```

Imagine it is like a gateKeeper which will allow the components to fetch data from context (_Box_).
<br>
In this code First we making ContextProvider that is going to be wrapper for components that are going to fetch data from Context. this function returns Provider and inside it there is children. This childrens are representing the Components that are going to wrap by Provider.
<br>
And the value prop it is taking the userData & setUserData in obj means in { } . here it saying that hey..! here's the values in Context (_Box_).**Here the we got the idea that the context contains the these values.**

Now this We are going to wrap to childrens means the components.

## Third step

Make the components that you want. In this case, here is Login and Profile component.

In this we are going to use the context.

The Login page

```javascript
import React, { useState } from "react";
import UserContext from "./UserContext";
import { useContext } from "react";
function Login() {
  const { setUserData } = useContext(UserContext);
  const [username, setUsername] = useState(""); // state management for input field
  const [password, setPassword] = useState(""); // state management for input field

  function handleSubmit(e) {
    e.preventDefault();
    setUserData({ username, password });
  }
  return (
    <>
      <div>Login</div>
      <input
        onChange={(e) => setUsername(e.target.value)}
        type="text"
        placeholder="username"
      />
      <input
        onChange={(e) => setPassword(e.target.value)}
        type="text"
        placeholder="password"
      />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}

export default Login;
```

In this we are using useContext hook to fetch data from context.

```javascript
const { setUserData } = useContext(UserContext);
```

And after fetching the setUserData method, we use it to update the data.

```javascript
function handleSubmit(e) {
  e.preventDefault();
  setUserData({ username, password });
}
```

the above upadtes the data in context. and through Profile page we show the data.

The Profile page

```javascript
import React, { useContext } from "react";
import UserContext from "./UserContext";

function Profile() {
  const { userData } = useContext(UserContext);
  if (!userData)
    return (
      <>
        <div>Profile:{userData}</div>
      </>
    );
  return <div>data:{userData.password}</div>;
}
export default Profile;
```

## The last but IMP.

We have to wrap the components which are going to have access of data.
here's the App.jsx file where we wrap the components (_Login and Profile_) by Provider. below is code.

```javascript
import React from "react";
import Login from "./components/Login";
import ContextProvider from "./components/ContextProvider";
import Profile from "./components/Profile";
function App() {
  return (
    <ContextProvider>
      <Login />
      <Profile />
    </ContextProvider>
  );
}

export default App;
```

Through this we will get concept of Context API.

## Make sure practice it with Project

🔵 **Multipage User Dashboard**

### Let me know if you’d like a tailored example for your project! 😊🚀
