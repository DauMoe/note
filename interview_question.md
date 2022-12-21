## Essential Skills & Requirements:
 - Experience in building web applications with video playback capabilities  
    +) Split to smaller part and load them when user watch loaded part  
    +) Use CDN to load faster  
    +) Use cache or store in local side. Apply with the resource that often be used  
    
 - Solid knowledge of web technologies (HTML/CSS/JavaScript) and frameworks in building responsive design and cross browser compatible
 - Solid understanding of JavaScript (ES6+)
 - Solid knowledge of React, React-Native, and similar technologies
 - Hands-on experience with popular JavaScript tools, frameworks and design principals, and up to date with the changing JavaScript ecosystem landscape
 - Experience in analyzing UI performance metrics and optimizing the implementation
 - Ability to perform and influence code reviews as well as technical design meetings
 - Thorough understanding of Software Development Lifecycle and methodologies

## Preferred Skills & Requirements:
 - Working experience with Scrum or similar agile methodologies
 - Experience with version control systems (e.g. Git) and understanding of branching models & strategies
 - Experience with docker and deployment tools
 - Experience with Xcode and Android Studio.

## Common Topics/Questions:
- React and ecosystem

- `Pure function` is function doesn't raise any side effect (update global variable) when executing

- Why React is popular than other library and frameworks?  
   - Angular is popular too but it's more complex than ReactJs. Developer can work with React as soon as they have basic knowledge about Js but Angular requires Typescript, RxJs and so on.   
   - Project structure of Angular is more complex than React too

- What is Virtual Dom? how it works and used inside React?  
   - Virtual DOM just an Js Object to revival (tái hiện) real DOM in some moment and it has the same element like real DOM (div, p, span, ...) <=> (Object div, Object p, ...)
   - Virtual DOM is a snapshot (a copy of real DOM) before updating and compare with a snapshot after updated. Thank for `Diffing` algorithm, React will find the difference and skip un-change elements
   - Benefit: VirtualDOM can run on multiple environment because `rendering` thing is split away from real DOM because virtual DOM just a Js Object 

- What is Reconciliation? Basic operations about reconcilers?
   - Reconciliation is the way React compare two Virtual DOM trees and decide what PART of elements should be changed. Suppose, we just change the className of component so React will update the className instead re-render this component. If the type of element is different, React will unmount the old component and create a new thing and so the same thing with the children components are inside it. If no different, no change
   - To do that, thank for helping of `Diffing` algorithm

   **Follow the document**
   - Reconciliation an API that you don't need to worry about how React update every element
   - First, whenever component is updated, new different tree is created and React has to figure out the most efficiently way to update the UI match with updated tree
   - Generic solutions finds the minimum elements that have changed however, the complexity of this algorithm is O(n^3) with N is number of elements => Big problem if N becomes a big number
   - To resolve that, React creates a new algorithm with the complexity is O(n)

- What is main goal for React Fiber?  or How react internally working? https://indepth.dev/posts/1008/inside-fiber-in-depth-overview-of-the-new-reconciliation-algorithm-in-react
   - **Main goal**: making the animation smooth. Reduce the complexity of Diffing algorithm
   - **Dive deep**
      - From version 16 and higher, React re-write the reconciliation. 
      - From version 15 and above, the algorithm is called `Stack reconciliation` because it works the same with stack (LIFO)
      - The thing that makes difference with `Stack Reconciliation`:
         - Pause the work and come back later if having any work higher priority
         - Assign the priority to different types of work
         - Reuse previous completed work result
         - Abort the work if it's no longer needed
      - So new version of React provides new functions like `matchesPriority(fiber, priority)`, `requestIdleCallback(lowPriorityWork)`, etc
      - Fiber structure can be refer [here](https://gist.githubusercontent.com/velotiotech/e479e75fe701d21d5c21ff3955203a35/raw/153b39a765e8dca79ae82408e2d7dff50a40d870/React-Fiber-type-defs.ts)

- Keys and why using keys?
   - Whenever you insert a new element into the list. The index will be changed. Without key, React will compare base on the index of element, compare type and the content inside elements, insert make the index change so the bad case, React will re-render all elements in this list and it's very bad.
   - Key to tell React the position of this element in previous and the next tree so React can increase the performance because it's no need to re-create all elements in the list
   - The key must be unique, stable and predictable. If the ket is unstable, DOM nodes will be unnecessarily re-render and once of causes raise bad performance
   => Shouldn't use key as index because if the list is re-order, index is changed and some elements will be re-render

- What is Ref in React?
   - It's a way to access the DOM nodes or React element that created by render method
  
- Why React use setState behide the screen
   - When you change the state, React has to re-render this value so if you change the value directly, React won't know when the components should be re-render
  
- What is immutable (bất biến) data? Why react state have to be immutable?
   - To make sure that the UI will updated whenever state change because React will doesn't know when the components should be re-rendered
  
- Why is it bad to access or mutate the state directly?
   - if modifying the state directly, it's NOT trigger re-render => the value on UI is NOT updated and all function or calculation NOT re-execute
  
- How many ways to copy object and what are they?
   - Spread operator ~ Object.assign()
   - Use JSON.parse(JSON.stringify({}));
   - Pros and cons:
      - JSON.stringify will lost the fields with value is function or promise
      - Spread operator is shallow copy. The value is object still has reference
  
- how can I render a responsive view? how do you know it has been resized or not?
   - Using media query of CSS or re-cal the components if size change. To detect size of window is changed, we can add a listener event to window and re-cal if the size of window smaller than a value what we define
  
- How React portals components work?
   - It will render component inside the `container` that is the second arg instead render this component as child inside the nearest parent component
   - But the behaviors of this element is the same with other element because it still exist in the React DOM tree. The event is fired inside 'portal' child will be catch by parent component
  
- How to implement the animation in React
   - I use CSS only like `animation` or `transform`
   - I hear about `useTransition` in React. Using for page route but I never use

- Problem solving - how to profile/debug the performance issue and how to resolve?
   - Use `Profiler API` or React Dev Tool that has Profiler inside so you can know what component takes a lot of time to render (re-render) and how many times

## React Component
- Functional and Class component difference in React?
   - Syntax:
      - Functional just a plain function in Js, receive props as params and return a React elements
      - Class must extend the React.Component and using render function to return React elements
   - Life Cycle:
      - Functional doesn't have this thing. We just revival it by using `useEffect`, `useMemo` or `React.memo`, so on
      - Class has life cycle
   - **State**
      - Functional only have the state when we call `useState`
      - Class always have default state no matter you create or not. If you console.log `this` pointer inside the `constructor` method, you will see `state: null`
   - **Ref**
      - Ref always be returned in class component
      - Functional doesn't have this thing
  
- What does PureComponent do? How is it different from typical traditional class components?
   - PureComponent and ReactComponent trigger re-render whenever props or state of this component is changed
   - **PureComponent will compare props when parent component re-render, ReactComponent is not**

- React Component lifecycle?
   - First, **initial** receive props
   - Second, **mounting** component will be render and mounted in this phase
   - Third, **update** the component will be re-render if having any change from props and state
   - Last, **un mounting** component will be remove when it's not used
  
- Use-case of using and not using getDerivedStateFromProps, getSnapshotBeforeUpdate
   - **getDerivedStateFromProps**: called whenever component is created or update props and state
  
- How are errors handled in React?
   - NOT sure what kind of errors that is mentioned here. Error about the logic, I will use `try-catch` to make sure every error is handle and they NOT make the app crash
   - To handle the condition inside JSX, I always use condition operator (ternary) and that thing makes sure no exception 
  
- What is React events? React events and HTML events differences?
   - HTML access real DOM and React access Virtual DOM instead
   - HTML events are written is lowercase, React events are camelCase
   - In HTML, inline event function must has `()` * **Open and Close parenthesis** *. In React, just take the function inside **the curly bracket** `{}`

- React controlled components and uncontrolled components differences? (refer [here](https://www.youtube.com/watch?v=ecY3QSxZZYY))
   - Controlled component: this component element value are controlled by React state. Element value and state are the same. Follow `single source of truth`
   - Uncontrolled component: the elements are controlled by DOM. Normally, you can use ref to access DOM node and get the value from that. But we have `two source of truth` here
   
- How to share the common logic across the React component?
   - Pass the logic function as a prop

- How to pass the data from parent to child component?
   - Use `props` to pass data from parent to child
  
### React Hook
- `useEffect` and `useLayoutEffect`
   - `useEffect` run after render component. Suppose, we click button -> setState -> re-render -> update UI -> trigger useEffect (if setState inside useEffect, component will be re-rendered again)
   - `useLayoutEffect` has the same function as `useEffect` BUT run **BEFORE** update the UI (before re-render). Same example, button is clicked -> setState -> render component -> trigger useLayoutEffect -> update UI

- Why couldn't use `async` inside `useEffect`? (refer [here](https://ultimatecourses.com/blog/using-async-await-inside-react-use-effect-hook))
   - React expects `useEffect` returns the cleanup function or nothing but `async` return a Promise so we will raise the memory leak here

- `useImperativeHandle`: customize the instance value and exposed *(expose: trưng bày)* to parent component when using `ref`

- Rules of Hook?
   - Only call hook on the top level. Not call inside loop, condition or nest function
   - Only call Hooks from React Functions or custom hook. DO NOT call from regular Js (Benefit: make sure that all stateful logic of this component is clearly visible from its source code)
   - Use ESLint, specific using `eslint-plugin-react-hooks`. That contains two above rules

- Hook at the very top of document (not inside conditionals) why?
   - Make sure hooks is called the same order each times component renders
   - Helping React can preserve correctly state of Hook when `useState` and `useEffect` is called

- How can I use the getSnapshot before updating in the functional component?
   - use `getSnapshotBeforeUpdate(prevProps, prevState)`, you can do any thing before component is updated. Any value returned by this lifecycle method will be passed as a parameter to `componentDidUpdate()`
   - `componentDidUpdate ` run after that
  
- What do react memo do inside react components? 
   - `React.memo` is HOC and it memoizes the passed in components so we can decide re-render the component or not. By default, comparative is shallow compare (so sánh nông), we can custom the comparative at second params as a callback
   *NOTE*: HOC is advantage skill in React. It doesn't React API. HOC is a function that receive a component as a param and return other component
  
- useMemo and useCallback use cases?
   - `useCallback(type => {}, deps)` is used when you want to memoize a **function** and return a new function if dependencies is changed => if components is re-render, function is NOT re-created (RETURN FUNCTION)
   - `useMemo(() => val), deps)` is used when you want to re-cal a value (Array, string, etc) and return a new value if dependencies is changed => if components is re-render, value is NOT re-cal (RETURN VALUE)
  
- How to implement the memoization function in Javascript (conceptually)? How do you hash dependencies?
   - Use an global Object as cache. Check this cache whenever you cal any formula => if existed ? get from cache : cal and save to cache
  
- How to store the scroll index when the user is scroll the page?
   - Can save the index to storage because it's not sensitive data

- Browser Engine
   - *To understand*
      - UI -> Browser Engine -> Rendering Engine -> (Networking, Js Interpreter, UI -> UI Backend) ![Browser Engine](./media/browser_engine.png)

   - The answer:
      - It's core component, working as a bridge between `User interface` and `Rendering engine`. Handle the rendering engine depends on input received from UI

- Why re-rendering or changing website on the browser is costly? or  How the browser behave when he has a change to the DOM what is the flow? (refer [here](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path) and [here](https://medium.com/technogise/dom-manipulation-in-browser-59b793bee559))
   - Repaint: 
      - just happen when changing only in the visibility of the element and not for changes in the layout => expensive because it requires browser search though all elements to determine what visible and what should displayed
      - Ex: add outline to elements, change background color, 
   - Reflow:
      - happen when changing the position, dimension of element => more critical then repaint because it's re-cal all element position and dimension, ... => leading to re-render part or all the document
      - Ex: multiple DOM change, display none, visibility: hidden, ...

   *Additional*
   - CRP:
      - DOM: construction is incremental. Using token turn into the DOM tree. Single DOM node start with `startTag` and end with `endTag`. This node contains data information about HTML Element. If having a `startTag` and `endTag` inside other `startTag` and `endTag`, we have a child DOM node. *The greater numbers of nodes, the longer following events in CRP will take*

      - CSS Object Model: contains information how to style the DOM, similar with DOM but different. *The browser blocks page rendering until it receives and processes all CSS* because CSS can be overwritten so content can't be rendered until CSSOM is complete

      - Render tree: capture both DOM and CSSOM tree and combine them into render tree. The browser checks every node from root of DOM tree and determine (xác định) which CSS will be attached. *Only capture visible content*

      - Layout: Render tree is built, layout becomes possible. Depend on screen size, determines how elements are positioned on the page, width and height each element, the relation between them. *Layout performance depends on DOM - greater nodes, longer layout take*

      -  Paint: painting the pixel on the screen. Just paint the impacted area, the browser just paint minimum are required
   - Optimizing performance
      - Minimum resource, async un-necessary resource by using async, defer or remove them 
      - Order the critical resources are loaded by priority, shortening the critical path length

- why the css transform is way better than margin left-right? (Refer: https://stackoverflow.com/questions/7108941/css-transform-vs-position)
   - Because transform not break the layout. Margin may break the elements width and height
   - Besides, transform is good for responsive than margin

- Vector / Frame - reduce lagginess or lightweight - animation engine - image with transparency etc so need to get rid of it to lighten it etc… otherwise in frame, there is lagged animation

- CSS object model?
   - It's a set of APIs allowing control CSS from Js. The same with DOM but for CSS rather than HTML. Allow to modify CSS dynamic

- why we should not use the important in CSS?
   - If all styles use `!important`, nothing is important
   - Un-expect behavior because nothing can higher priority than `!important`

- How to measure the browser web performance? what are the solution to improve it?
- Have you use the srcset of an image?  

## State management
- Why are we the state management (Redux)? or why does redux was built? what problem does Redux solve?
   - Know exactly where state is store, they will be scattered *(rải rác)* everywhere if app doesn't have state management
   - Clearly state update flow and control update by one way flow
   - Easy to understand

- why Flux is multi stores while redux is only single store?
   - Store in flux use to specific data. Like PostStore, MessageStore, .... ([Refer Flux](https://www.freecodecamp.org/news/how-to-use-flux-in-react-example/))
   - Redux doesn't follow this way. Redux only has one store but having a lot of reducer. It's the same when you access all store in Flux in one place

- React Context and Redux. What is the different? what is your prefer?
   - Different:
      - Context:  
         - This is designed to share data as global state
         - All components inside Context Provider will re-render immediately -> Should create multiple context to manager -> DO NOT update frequency
         - Good for simple flows data changes
      - Redux:
         - Designed for state management purpose -> cover this thing very well -> can update frequency
         - Easy to understand the state change flow because the states are stored one place
   => prefer redux because when app is scaled, we have to use Redux so why don't we use it in the first time?

- Principles of Redux? Describe the redux workflow?
   - Principles:
      - Single source of truth: global state of app should be stored in one place. Prevent duplicate data many places and easier to debug and inspect changing
      - State is read-only: only one-way to change state. That dispatches an action. Follow this way, the data is not overwrite by UI, UI just trace the update of state
      - Change are made with pure reducer functions: Reducer function is pure function that receive previous state and an action. Return the next state
   - Redux workflow: view -> dispatch action -> update state in store -> re-render view -> ...

- **Why reducers were invited in the first place? Build to guard the data and monitor/control the side effects**
  
- Provide solutions for not re-render component when the redux store change
   - By default, Redux uses shallow equality check between props that generated by `mapStateToProps` and `mapDispatchToProps` args passed to `connect(mapStateToProps, mapDispatchToProps)`. But some case, this equality doesn't helpful 

- Create your own middleware with Redux?
   - Middleware is triggered before reducer receives an action AND after an action is dispatched

- How can I make an Ajax request (api request) with redux?
   - You can `dispatch` an action after AJAX request done

- Why Redux Thunk easier than Saga?
- Redux Saga? Why is it invented how is it different from Redux Thunk or something like that? Side effect tasks?

- How saga work in basically?
   - Saga uses for handle side effect like call API, read, write file, etc
   - Main sage splits into two different things: workers & watchers
      - Watchers: watching every action that is dispatched to redux store. If it matches with one of actions, this action will be assigned to workers

- Use generator for such purpose and why do we use generator functions?
   - generator function make your code look more synchronous => easy to read, write and test

- Saga: What are differences between call and put action?
   - `call` blocks the effect. Waiting for promise resolved before moving to next step
   - `put` NOT block effect and saga can move to next step. `Action` will be dispatched internal

- SSG: Static Site Generation
   - Site is generated and cache in CDN. Very fast

- SSR: Server side rendering
   - Page will be rendered each request

- Have you working with NextJS?

- How to render the data on server side?
   - `getServerSideProps`: use for SSR, never run on browser. Pass data to component as props
   - `getStaticProps`: use for SSG (static site generation)
   - `getInitialProps`: working as `componentDidMount` but can working with SSR
- Enhance SEO
- What is semantic HTML?
   - Thẻ HTML ứng với nội dung được chứa như thẻ section (chia ra các phần riêng biệt của thẻ HTML), article (chứa các nội dung độc lập, bao gôm đầy đủ ngữ cảnh), nav (chưa các thẻ điều hướng đến các section cụ thể trong trang), aside, header, footer, div, main, body

- Security
- How to check the NPM packages vulnerability? 
- Have you worked with Synk
- Mobile development and other
- When the libraries is deprecated, how to refactor or enhancement code?
- Have you worked with PWA?
- Communication between native mobile app and webview (web app)
- Build, Sign app with key, Uploading APK store?
- Did you write in objective C or anything Apple Native / Swift?
- Deal with Android studio and xCode?
- How do you learn new tech or new library? (twitter channel, documentations, articles research, online course platforms, youtube conference for react etc…)
