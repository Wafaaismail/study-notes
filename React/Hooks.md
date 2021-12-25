## React Hooks 
> Hooks are features in react to allow writting react features without class in function comp 
> only used in function components

## why
- avoid confusion of this keyword in classes 
- Allow you to reuse stateful logic without change the code 
- organize the logic inside the component into reusable isolated units (related code put together to eleminate the bugs)

## Rules of Hooks 
- only call hooks at the top level (Not inside functions,loops,conditions)
- only call hooks from functional component 
_______
## use State 
 **Lets you add satte to Functional components**
**updating state cause the component to rerender**

> const [state,setState] = useState(0)
> state => the current value of state variable 
```state variable can be number , string , object or array ```
> setState => the function that update state "the setter function"
> 0  => initial value

### simple example 
```js
  const [counter, setcounter] = useState(0);
  return (
    <div>
      <button onClick={() => setcounter(counter + 1)}>count {counter}</button>
    </div>
  );
```

### update state with prev state 
when we need to update state depending on the prev state value it's safer to use this form of set state which  take a function that can handle the state object .
``` setcounter(prevCount => prevCount + 1)```

### use state with Object 
> **use state doesnot automaticlly merge and update the objects you have to do it manullay using spreed operator**
```js
import { useState } from "react";
export default function DealingWithStateObject() {
  const [name, setName] = useState({firstName: "",lastName: ""});
  return (
    <div>
      <input
        type="text"
        value={name.firstName}
        onChange={(e) => setName({ ...name, firstName: e.target.value })}
      />
      <input
        type="text"
        value={name.lastName}
        onChange={(e) => setName({ ...name, lastName: e.target.value })}
      />
      <h2>firstName:{name.firstName}</h2>
      <h2>lastName: {name.lastName}</h2>
    </div>
  );
}
```
### use state with Array 
> **use state doesnot automaticlly append value to the end of the array s you have to do it manullay using spreed operator**

```js
setItems([
        ...items, 
        {
        id: items.length,
        value: Math.floor(Math.random() * 10) + 1
        }
    ]);
```
____
## use Effect 
**lets you performe the side effects in functional components.
its a replacement of life cycle methodds componentdidmount(), componentdidupdatet(), componentwillunmount()
we can write more than useEffect in the same component**


```js
  // run every time after the component render 
  useEffect(() => {
    document.title = `You have clicked ${counter} Times`;
  });
```

#### Conditionally run effects 
run the useEffect function everytime after the component render may cause a performance issue so we need it to run conditionally ,
By using the second parameter of useEffect which is an array of props or state variable to watch and run the effect only if those variables changes .
``` 
//run only if counter value changes 
  useEffect(() => {
    document.title = `You have clicked ${counter} Times`;
  },[counter]);
```

####  Run effects only once "mimic of componentDidMount()"
By passing an empty array as a second parameter of useEffect 
```js
// run only in the first render 
 useEffect(() => {
    window.addEventListener("mousemove", setMousePosition);
  },[]);
```

####  useEffect with cleanup "componentWillUnMount"
this may be for remove event listeners , timers ,subscribtions 
when the component removed from dom we need to remove all the related code as it cause a memory leak and can not update it's state 

so we use return of useEffect function as a clean up function .
```js
useEffect(() => {
    window.addEventListener("mousemove", setMousePosition);
    // clean up 
    return ()=>{
      window.removeEventListener("mousemove",setMousePosition)
    }
  }, []);
```

#####  Fetching data with useEffect

Fetch data once the component mount  and set it in state 
```js
  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(({data}) => {
        setPosts(data)
      })
      .catch((err) => console.log({ err }));
  },[]);
```
______
 ## use Context
 **Provide a way to pass data through the component tree without having to pass props down manually at every level**
 
 ##### 3 steps to implement context 
 > 1- create context  
 > 2- wrap children with provider and add value to it 
 > 3-consume the context value 
 
 but the problem come when we use more than one context , alot of unncessrcy code , use context hook fix this problemm 
 
 use Context => replace the third step with simple way just pass your context to use Context 
 ```js 
 const user = useContxet(userContext )
 ``` 
```js
    <>
      <Context.Provider value={ "Initial Value" }>
        <Child /> {/* Child inside Provider will get "Initial Value" */}
      </Context.Provider>
        <Child2 /> {/* Child outside Provider will get "Default Value" */}
    </>
```
## use CallBack 
**used for performance optimization**
> cache the provided func itself and return a func
```js 
// handleClick is a function 
  const handleClick = useCallback(() => {
    // handle the click event
  }, []);
```
## use Memo
**used for performance optimization**
we need to tell react to not calculate value when it is not necessary 
> invoke the provided func itself and return cache the result 

```js 
// even is value returen from this func 
const even = useMemo(()=>{
    return number % 2 
},[number])
```

## use Ref
**make it possible to access dom node directly from func component**

1-create ref with use ref hook 
2- assign this ref to a component needed then use it 
```js 
const inputRef = useRef(null)

<input type="text" ref={inputRef}/>

//use it as 
inputRef.current.focus();
```
also useRef can save mutable object through rendering not causeing any rerender

## custom Hooks 
js function whose name start with "use "

used to share logic between componnents alternative of hoc and render props
