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
   - Simple: Increase the Diffing algorithm O(n^3) => O(n)
   - From version 16 and higher, React implements a new thing is called `Fiber`

- Keys and why using keys?
   - Whenever you insert a new element into the list. The index will be changed. Without key, React will compare base on the index of element, compare type and the content inside elements, insert make the index change so the bad case, React will re-render all elements in this list and it's very bad.
   - Key to tell React the position of this element in previous and the next tree so React can increase the performance because it's no need to re-create all elements in the list
   - The key must be unique, stable and predictable. If the ket is unstable, DOM nodes will be unnecessarily re-render and once of causes raise bad performance
   => Shouldn't use key as index because if the list is re-order, index is changed and some elements will be re-render

- What is Ref in React?
  
- Why React use setState behide the screen
   - When you change the state, React has to re-render this value so if you change the value directly, React won't know when the components should be re-render
  
- What is immutable (bất biến) data? Why react state have to be immutable?
   - To make sure that the UI will updated whenever state change because React will doesn't know when the components should be re-rendered
  
- Why is it bad to access or mutate the state directly?
   - if modifying the state directly, it's NOT trigger re-render => the value on UI is NOT updated and all function or calculation NOT re-execute
  
- How many ways to copy object and what are they?
   - Spread operator 
   - Use JSON.parse(JSON.stringify({}))
   - Use Object.assign({}, {});
  
- how can I render a responsive view? how do you know it has been resized or not?
   - Using media query of CSS or re-cal the components if size change. To detect size of window is changed, we can add a listener event to window and re-cal if the size of window smaller than a value what we define
  
- How React portals components work?
   - It will render component inside the `container` that is the second arg instead render this component as child inside the nearest parent component
   - But the behaviors of this element is the same with other element because it still exist in the React DOM tree. The event is fired inside 'portal' child will be catch by parent component
  
- How to implement the animation in React
   - I use CSS only like `animation` or `transform`

- Problem solving - how to profile/debug the performance issue and how to resolve?
- React Component
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
  
- What does Pure component do? How is it different from typical traditional class components?
- React Component lifecycle?
   - First, **initial** receive props
   - Second, ** component will be render and mounted in this phase
   - Third, **update** the component will be re-render if having any change from props and state
   - Last, **un mounting** component will be remove when it's not used
  
- Use-case of using and not using getDerivedStateFromProps, getSnapshotBeforeUpdate
   - **getDerivedStateFromProps**: called whenever component is created or update props and state
  
- How are errors handled in React?
   - NOT sure what kind of errors that is mentioned here. Error about the logic, I will use `try-catch` to make sure every error is handle and they NOT make the app crash
   - To handle the condition inside JSX, I always use condition operator (ternary) and that thing makes sure no exception 
  
- What is React events? React events and HTML events differences?
- React controlled components and uncontrolled components differences?
- How to share the common logic across the React component?
- How to pass the data from parent to child component?
   - Use `props` to pass data from parent to child
  
- React Hook
- Rules of Hook?
- Hook at the very top of document (not inside conditionals) why?
- How can I use the getSnapshot before updating in the functional component?
   - use `getSnapshotBeforeUpdate(prevProps, prevState)`, you can do any thing before component is updated. Any value returned by this lifecycle method will be passed as a parameter to `componentDidUpdate()`
   - `componentDidUpdate ` run after that
  
- What do react memo do inside react components? `React.memo` is HOC and it memoizes the passed in components so we can decide re-render the component or not. By default, comparative is shallow compare (so sánh nông), we can custom the comparative at second params as a callback
   *NOTE*: HOC is advantage skill in React. It doesn't React API. HOC is a function that receive a component as a param and return other component
  
- useMemo and useCallback use cases?
   - `useCallback(type => {}, deps)` is used when you want to memoize a **function** and return a new function if dependencies is changed => if components is re-render, function is NOT re-created (RETURN FUNCTION)
   - `useMemo(() => val), deps)` is used when you want to re-cal a value (Array, string, etc) and return a new value if dependencies is changed => if components is re-render, value is NOT re-cal (RETURN VALUE)
  
- How to implement the memoization function in Javascript (conceptually)? How do you hash dependencies?
- How to store the scroll index when the user is scroll the page?
- Browser Engine
- Why re-rendering or changing website on the browser is costly? or  How the browser behave when he has a change to the DOM what is the flow?
- why the css transform is way better than margin left-right? (Refer: https://stackoverflow.com/questions/7108941/css-transform-vs-position)
- Vector / Frame - reduce lagginess or lightweight - animation engine - image with transparency etc so need to get rid of it to lighten it etc… otherwise in frame, there is lagged animation
- CSS object model?
- why we should not use the important in CSS?
- How to measure the browser web performance? what are the solution to improve it?
- Have you use the srcset of an image?  

## State management
- Why are we the state management (Redux)? or why does redux was built? what problem does Redux solve?
- why Flux is multi stores while redux is only single store?
- React Context and Redux. What is the different? what is your prefer?
- Principles of Redux? Describe the redux workflow?
- Why reducers were invited in the first place? Build to guard the data and monitor/control the side effects
- Provide solutions for not re-render component when the redux store change
- Create your own middleware with Redux?
- How can I make an Ajax request (api request) with redux?
- Why Redux Thunk easier than Saga?
- Redux Saga? Why is it invented how is it different from Redux Thunk or something like that? Side effect tasks?
- Use generator for such purpose and why do we use generator functions?
- Saga: What are differences between call and put action?
- Server side rendering
- Have you working with NextJS?
- How to render the data on server side?errors
- Enhance SEO
- What is semantic HTML?
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
