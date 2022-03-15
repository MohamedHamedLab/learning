# React Hooks

### UseMemo

```jsx
const reverseWord = (word) => {

return word.spplit("").reverse().join("")

}

const title = "test string";

const titleReversed = useMemo(() => reverseWord(title), [title])

//Use

return (

<h1>{titleReserved}</h1>

)
```

### UseRef

```jsx
const hRef = useRef()

return (

<h1 onClick={()=> hRef.current.classList.add("new-class")} />

)
```

### Custom Hooks

```jsx
function useTitleInput (initalValue) {

const [value, setValue] = useState (initalValue);

useEffect (() => {});

return [value, setValue];

}

//Use

const [name, setName] = useTitleInput("")
```

### Composing

```jsx
HOC return Wrapped component with injected Props

const hasProps = injectedProps => WrappedComponent => {

const HasProps = props => <WrappedComponent {...injectedProps} {...props} />

return HasProps

}

//Use

hasProps({sample: 'Sample Prop'})(Component)
```

**UseContext**