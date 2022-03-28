**#React Best Practice**
#React JS
React is a JavaScript library created for building fast and interactive user interfaces for web and mobile applications. It is an open-source, component-based, front-end library responsible only for the application’s view layer. In Model View Controller (MVC) architecture, the view layer is responsible for how the app looks and feels.

##Abstraction:
React thrives on reusability. When talking about React best practices, the term abstraction comes up a lot. Abstraction means that there are portions of a large component or application that can be taken away, divided into multiple functional components, and then imported into the larger component. Making a component as simple and small as possible, often so it only serves one purpose, increases your chance for the code to be reusable.
##Component:
React, JSX principles instruct you to create a single target-oriented, small, and loosely coupled component. It makes the task of building UIs much easier. You can see a UI broken down into multiple individual pieces called components and work on them independently.

**Advantage of small component:**
1. The small component can be reused in a better way.
2. Easy to maintain.
3. Easy to unit test and debug.

##Naming Convention:
There are three main naming conventions in React that should be considered best practice.
1. Component name should be PascalCase – capitalized in camelCase as well and named for their function and not the specific application feature (in case you change it later).
2. Elements that need keys should be unique, non-random identifiers (such as individual cards or entries in a card deck or List). It is best practice to not use just indexes for keys. It is legal to have a key assignment that is made of a concatenation of two different object properties.
3. Methods should be in camelCase and be named for their function and not be application-specific.

##Write Unit test Cases:
We should write a unit test for each component. This would be very easy as almost all the components created are just calling other components and passing props. The only thing needed is to test that the correct components are rendered, and the correct props are passed. Additionally, we should test that toggle works as expected to show the comments.

##CSS Preprocessors:
CSS preprocessors are scripting languages that extend the default capabilities of CSS. They enable us to use logic in our CSS code, such as variables, nesting, inheritance, mixins, functions, and mathematical operations. CSS preprocessors make it easy to automate repetitive tasks, reduce the number of errors and code bloat, create reusable code snippets, and ensure backward compatibility.

##Setup linting rules:
JSLint takes a JavaScript source and scans it. If it finds a problem, it returns a message describing the problem and an approximate location within the source. The problem is not necessarily a syntax error, although it often is. JSLint looks at some style conventions as well as structural problems. It does not prove that your program is correct. It just provides another set of eyes to help spot problems.

##Web Accessibility:
Web accessibility (WCAG, WAI-ARIA, Semantic HTML) is the design and creation of websites that can be used by everyone. Accessibility support is necessary to allow assistive technology to interpret web pages. React fully supports building accessible websites, often by using standard HTML techniques.

##Minify Production Build:
If you’re benchmarking or experiencing performance problems in your React apps, make sure you’re testing with the minified production build.
By default, React includes many helpful warnings. These warnings are very useful in development. However, they make React larger and slower so you should make sure to use the production version when you deploy the app.

##Cashed Static content “Offline”:
Many internet programs have an “offline mode” when disconnected from a network. A browser can still show pages that are either already loaded or stored locally. 
Eg. Email clients let users view messages they have already downloaded when not connected to a network. They can also reply or compose new messages. When a user reconnects to the network, these messages will automatically sync to our servers.

#Security
##XSS protection:
Use default data binding with curly braces {} and React will automatically escape values to protect against XSS attacks. Note that this protection only occurs when rendering text content and not when rendering HTML attributes. Use JSX data-binding syntax {} to place data in your elements.

##DOM Sanitization:
DOMPurify sanitizes HTML and prevents XSS attacks. You can feed DOMPurify with a string full of dirty HTML and it will return a string (unless configured otherwise) with clean HTML. DOMPurify will strip out everything that contains dangerous HTML and thereby prevent XSS attacks and other nastiness. We use the technologies that the browser provides and turn them into an XSS filter. 

##Dangerous library code:
Library code is often used to perform dangerous operations like directly inserting HTML into the DOM. Review library code manually or with linter to detect unsafe usage of React’s security mechanisms.

##Error Boundaries:
The most distinctive and React-specific type of error handling is what is known as error boundaries. This feature was introduced in React 16 and allows you to define components that act as error-catching mechanisms for the component tree.

##Secure Against DDoS Attacks:
The vulnerable security concerns take place when the whole application state management has loopholes, and it masks the IPs. This will restrict the communication caused due to the termination of services. Here are some methods to stop this:

1. Limitation of rate on APIs- This will add limitations to the number of requests for a given IP from a specific source with a complete set of libraries using the Axios-rate limit.
2. Add app-level restrictions to the API.

##SQL Injection:
This attack is related to data manipulation. Due to this vulnerability, attackers can modify any data with or without the user’s permission or can extract any confidential data by executing arbitrary SQL code.
**Solution:** To eliminate SQL injection attacks, first, validate API call functions against the respective API schemas. To handle the issue of time-based SQL injection attacks, you can use timely validation of the schema to avoid any suspicious code injections.

##Direct DOM Access:
Accessing the DOM to inject content into DOM nodes directly should be avoided. Use dangerouslySetInnerHTML if you must inject HTML and sanitize it before injecting it using DOM-purify. 
Avoid using refs and findDomNode() to access rendered DOM elements to directly inject content via innerHTML and similar properties or methods.

**General Practice:**
```ts
this.myRef.current.innerHTML = attackerControlledValue;
```

**Best Practice:**
```ts
import purify from "dompurify";
<div dangerouslySetInnerHTML={{__html:purify.sanitize(data) }} />
```

##Dangerous URLs:
URLs can contain dynamic script content via JavaScript: protocol URLs. Use validation to assure your links are HTTP: or HTTPS: to avoid JavaScript: URL-based script injection. Achieve URL validation using a native URL parsing function then match the parsed protocol property to an allow list.

**General Practice:**
```ts
import React from 'react';  
const Login = () => {
  return <a href={attackerControlled}>Click here!</a>;
}  
export default Login;
```

**Best Practice:**
```ts
import React from 'react';  
const Login = () => {
  function validateURL(url) {
    const parsed = new URL(url)
    return ['https:', 'http:'].includes(parsed.protocol)
  }  
  return <a href={validateURL(url) ? url : ''}>Click here!</a>
}  
export default Login;

```

#Performance
##Use Functional Components:
A lot of developers get confused about whether they should go with a Class component or functional component. If you aren’t using the life cycle method, then it’s efficient to write functional components. Functional components are much easier to read and test because they are plain JavaScript functions without state or life cycle methods. Some of the advantages are as follows:

1. Fewer lines of code and better performance
2. Easier to read, easy to understand, and easy to test.
3. No need to use ‘this’ binding.
4. Easier to extract smaller components.

**General Practice**
```ts
import React, { Component } from 'react';
  
class Button extends Component {
  render() {
    const { btnLabel, cssClass, onClick } = this.props;
    return (
      <button onClick={onClick} className={cssClass}>{btnLabel}</button>
    );
  }
}  
export default Button;
```

**Best Practice:**
```ts
import React from 'react';
  
const Button = ({ btnLabel, cssClass, onClick }) => {
  return (
    <button onClick={onClick} className={cssClass}>
      {btnLabel}
    </button>
  );
}  
export default Button;

```

##Use Fragments:
Always use Fragment over HTML tag. It keeps the code clean and is also beneficial for performance because one less node is created in the virtual DOM.

**General Practice:**
```Ts
import React from 'react';
function App() {
  return (
    <div>
      <div>Learn </div>
      <div>React</div>
    </div>
  );
}

export default App;
```

**Best Practice:**
```ts
import React from 'react';
function App() {
  return (
    <>
      <div>Learn </div>
      <div>React</div>
    </>
  );
}

export default App;

```
##Use React.lazy:
React .lazy takes a function that must call a dynamic import() and render inside a Suspense component, which allows us to show some fallback content (such as a loading indicator) while we’re waiting for the lazy component to load.

**General Practice:**
```ts
import React from 'react'
import App from './App'
export default function Best() {
    return (
        <div>
            <App />
        </div>
    )
}
```

**Best Practice:**
```ts
import React, {lazy, Suspense} from 'react';
const App = lazy(()=> import('./App'));
export default function Best() {
    return (
        <Suspense fallback={<>Loading...</>}>
            <App />
        </Suspense>
    )
}
```

##Use React.memo:
React.PureComponent and Memo can significantly improve the performance of your application. They help us to avoid unnecessary rendering.

**General Practice**
```ts
import React from 'react';
export function User({ name, email }) {
  return (
    <>
      <div>Name: {name}</div>
      <div>Email: {email}</div>
    </>
  );
}
// memoize the component
export default User;
```

**Best Practice**
```ts
import React from 'react';
export function User({ name, email }) {
  return (
    <>
      <div>Name: {name}</div>
      <div>Email: {email}</div>
    </>
  );
}
// memoize the component
export default React.memo(User);

```
##Conditional rendering:
There are a couple of great ways to do the conditional rendering. Short circuit operators are a very short and easy way to do conditional rendering:
```ts
import React from 'react';
const Counter = ({ count }) => {
  return (
    <>
      {count && <h1>Count: {count}</h1>}
    </>
  )
}
export default Counter;
```

#Code Optimization
##Consolidate DOM duplicate:
React best practices instruct you to keep code brief, precise, and easy to understand. One way to do this is to avoid code duplication (DRY). for that, we can restrict ourselves to write concise and reusable code.

**General Practice:**
```ts
import React from 'react';
const Button = () => {
  return (
    <ul>
      <li>Home</li>
      <li>About</li>
      <li>Contact</li>
    </ul>
  );
}  
export default Button;
```

**Best Practice:**
```ts
import React from 'react';
const Button = () => {
  const navList = ['Home', 'About', 'Contact'];
  const renderNav = () => navList.map(nav => <li>nav</li>)
  return (
    <ul>{renderNav()}</ul>
  );
}  
export default Button;

```

##Use Ternary Operators:
Let’s say you want to load particular component details based on the session.

**General Practice:**
```ts
import React from 'react';
  const renderName = () => {
    if(session){
      return <Dashboard />
    }else{
      return <Login />
    }
  }
```

**Best Practice**
```ts
import React from 'react';
const renderName = () => session ? <Dashboard />:<Login />
```  

##Take Advantage of Object Literals:
Object literals can help make our code more readable. Let’s say you want to show three types of users based on their roles. 

**General Practice:**
```ts
const role = "ADMIN";
switch(role){
  case 'ADMIN':
    return <Admin />
  case 'OWNER':
    return <Owner />
  case 'MEMBER':
    return <Member />
}
```
**Best Practice:**
```ts
const role = "ADMIN";
const components={ ADMIN, Owner, Member }
const Component = components[role];
```

##Take Advantage of Object Destructuring:
Use object destructuring to your advantage. Let’s say you need to show a user’s details.

**General Practice:**
```ts
import React from 'react';
function App(props) {
  return (
    <div className="App">
      <div>First Name: {props.fName}</div>
      <div>First Name: {props.lName}</div>
    </div>
  );
}
export default App;
```

**Best Practice:**
```ts
import React from 'react';
function App(props) {
  const {fName, lName} = props;
  return (
    <div className="App">
      <div>First Name: {fName}</div>
      <div>First Name: {lName}</div>
    </div>
  );
}
export default App;
```
String Props Don’t Need Curly Braces: 
When passing string props to a children component.

##Use Template Literals:
Use template literals to build large strings. Avoid using string concatenation. It’s nice and clean.

**General Practice:**
```ts
  <div className="App">
      {'My first name is '+fName + ' and last name is '+ lName}
  </div>
```

**Best Practice:**
 ```ts 
  <div className="App">
      {`My first name is ${fName} and last name is ${lName}`}
  </div>
```
##Use Implicit return:
Use the JavaScript feature of implicit return to write beautiful code. Let’s say your function does create a user list and returns the result.

**General Practice:**
 ```ts
  const renderUser = (users) => {
    return users.map(user=> <div>{user}</div>);
  }
```

**Best Practice:**
```ts
  const renderUser = (users) => users.map(user=> <div>{user}</div>);
```

##JSX in Parentheses:
If your component spans more than one line, always wrap it in parentheses.

**General Practice:**
```ts
  return <Main>
    <Child />
  </Main>
 ```

**Best Practice:**
```ts
  return (
    <Man>
      <Child />
    </Main>
  )
```  
##Self-Closing Tags:
If your component doesn’t have any children, then use self-closing tags. It improves readability.
```ts
   <User />
 ```

#Tools & Extensions

##Code Snippet extensions:
Code snippets help to keep up with the best and most recent syntax. It also helps to keep your code relatively bug-free, so this is one of the React best practices that we should follow. There are many snippet libraries that you can use, like, ES7 React, Redux, JS Snippets, etc.

##React Developer tools:
React Developer tools’ is a DevTool extension built by the React team. It surely needs no introduction but there’s one feature I’d like to bring to your attention — the “Highlight Updates”. That’s a great feature for tracking which component gets re-rendered. It does this by coloring the boundaries of components, whenever they are re-rendered.

##Redux DevTools Extension:
Working with redux may be quite intimidating with fancy terminologies like actions, reducers, middleware, store, etc. But Redux DevTools extension can help you a lot in visualizing all the complex events that are happening in a redux application and communication medium between your react application and redux root reducer.

 ##Lighthouse Extension:
Lighthouse is an open-source, automated tool for improving the quality of web pages. You can run it against any web page, public or requiring authentication. It has audits for performance, accessibility, progressive web apps, SEO, and more.
