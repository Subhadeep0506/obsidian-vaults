# Kent C. Dods React Course Notes

# 1. React Hooks

## a. `useState`

### Background

Normally an interactive application will need to hold state somewhere. In React, you use special functions called "hooks" to do this. Common built-in hooks include:

-   `React.useState`
-   `React.useEffect`
-   `React.useContext`
-   `React.useRef`
-   `React.useReducer`

Each of these is a special function that you can call inside your custom React component function to store data (like state) or perform actions (or side-effects). There are a few more built-in hooks that have special use cases, but the ones above are what you'll be using most of the time.

Each of the hooks has a unique API. Some return a value (like `React.useRef` and `React.useContext`), others return a pair of values (like `React.useState` and `React.useReducer`), and others return nothing at all (like `React.useEffect`).

Here's an example of a component that uses the `useState` hook and an onClick event handler to update that state:

```jsx
function Counter() {
  const [count, setCount] = React.useState(0)
  const increment = () => setCount(count + 1)
  return <button onClick={increment}>{count}</button>
}
```

`React.useState` is a function that accepts a single argument. That argument is the initial state for the instance of the component. In our case, the state will start as `0`.

`React.useState` returns a pair of values. It does this by returning an array with two elements (and we use destructuring syntax to assign each of those values to distinct variables). The first of the pair is the state value and the second is a function we can call to update the state. We can name these variables whatever we want. Common convention is to choose a name for the state variable, then prefix `set` in front of that for the updater function.

State can be defined as: data that changes over time. So how does this work over time? When the button is clicked, our `increment` function will be called at which time we update the `count` by calling `setCount`.

When we call `setCount`, that tells React to re-render our component. When it does this, the entire `Counter` function is re-run, so when `React.useState` is called this time, the value we get back is the value that we called `setCount` with. And it continues like that until `Counter` is unmounted (removed from the application), or the user closes the application.

```jsx 
// Exercise 1
function Greeting() {
  const [name, setName] = React.useState("")

  function handleChange(event) {
    setName(event.target.value)
  }

  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}
```

### Extra Credit

#### 1. 💯 accept an `initialName`

Make the `Greeting` accept a prop called `initialName` and initialize the `name` state to that value.
```jsx
function Greeting({initialName}) {
  const [name, setName] = React.useState(initialName)

  function handleChange(event) {
    setName(event.target.value)
  }

  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}

function App() {
  return <Greeting initialName={'George'} />
}
```

## b. `useEffect`: persistent state

##### Background

`React.useEffect` is a built-in hook that allows you to run some custom code after React renders (and re-renders) your component to the DOM. It accepts a callback function which React will call after the DOM has been updated:

```javascript
React.useEffect(() => {
  // your side-effect code here.
  // this is where you can make HTTP requests or interact with browser APIs.
})
```

Feel free to take a look at `src/examples/hook-flow.png` if you're interested in the timing of when your functions are run. This will make more sense after finishing the exercises/extra credit/instruction.

### Exercise

In this exercise, we're going to enhance our `<Greeting />` component to get its initial state value from localStorage (if available) and keep localStorage updated as the `name` is updated.

```jsx
function Greeting({initialName = ''}) {
  const [name, setName] = React.useState(
    window.localStorage.getItem('name') || initialName,
  )

  React.useEffect(() => {
    window.localStorage.setItem('name', name)
  })

  function handleChange(event) {
    setName(event.target.value)
  }
  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}
```

### Extra Credit

#### 1. 💯 lazy state initialization

Right now, every time our component function is run, our function reads from localStorage. This is problematic because it could be a performance bottleneck (reading from localStorage can be slow). And what's more we only actually need to know the value from localStorage the first time this component is rendered! So the additional reads are wasted effort.

To avoid this problem, React's `useState` hook allows you to pass a function instead of the actual value, and then it will only call that function to get the state value when the component is rendered the first time. So you can go from this: `React.useState(someExpensiveComputation())` To this: `React.useState(() => someExpensiveComputation())`

And the `someExpensiveComputation` function will only be called when it's needed!

Make the `React.useState` call use lazy initialization to avoid a performance bottleneck of reading into localStorage on every render.

```jsx
function Greeting({initialName = ''}) {
  const [name, setName] = React.useState(
    () => window.localStorage.getItem('name') || initialName,
  )

  React.useEffect(() => {
    window.localStorage.setItem('name', name)
  })

  function handleChange(event) {
    setName(event.target.value)
  }
  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}
```

> Learn more about [lazy state initialization](https://kentcdodds.com/blog/use-state-lazy-initialization-and-function-updates)

#### 2. 💯 effect dependencies

[Production deploy](https://react-hooks.netlify.app/isolated/final/02.extra-2.js)

The callback we're passing to `React.useEffect` is called after _every_ render of our component (including re-renders). This is exactly what we want because we want to make sure that the `name` is saved into localStorage whenever it changes, but there are various reasons a component can be re-rendered (for example, when a parent component in the application tree gets re-rendered).

Really, we _only_ want localStorage to get updated when the `name` state actually changes. It doesn't need to re-run any other time. Luckily for us, `React.useEffect` allows you to pass a second argument called the "dependency array" which signals to React that your effect callback function should be called when (and only when) those dependencies change. So we can use this to avoid doing unnecessary work!

Add a dependencies array for `React.useEffect` to avoid the callback being called too frequently.

```jsx
React.useEffect(() => {
	window.localStorage.setItem('name', name)
}, [name]) // Here name is mentioned as a dependency
```

#### 3. 💯 custom hook

[Production deploy](https://react-hooks.netlify.app/isolated/final/02.extra-3.js)

The best part of hooks is that if you find a bit of logic inside your component function that you think would be useful elsewhere, you can put that in another function and call it from the components that need it (just like regular JavaScript). These functions you create are called "custom hooks".

Create a custom hook called `useLocalStorageState` for re-usability of all this logic.

```jsx
const useLocalStorageState = (key, defaultValue = '') => {
  const [state, setState] = React.useState(
    () => window.localStorage.getItem('name') || defaultValue,
  )

  React.useEffect(() => {
    window.localStorage.setItem('name', state)
  }, [key, state])

  return [state, setState]
}

function Greeting({initialName = ''}) {
  const [name, setName] = useLocalStorageState('name', initialName)

  function handleChange(event) {
    setName(event.target.value)
  }
  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}
```

#### 4. 💯 flexible localStorage hook

Take your custom `useLocalStorageState` hook and make it generic enough to support any data type (remember, you have to serialize objects to strings... use `JSON.stringify` and `JSON.parse`). Go wild with this!

```jsx
const useLocalStorageState = (
  key,
  defaultValue = '',
  {serialize = JSON.stringify, deserialize = JSON.parse},
) => {
  const [state, setState] = React.useState(() => {
    const valueInLocalStorage = window.localStorage.getItem(key)
    if (valueInLocalStorage) return deserialize(valueInLocalStorage)

    return typeof defaultValue === 'function' ? defaultValue() : defaultValue
  })

  React.useEffect(() => {
    window.localStorage.setItem('name', state)
  }, [key, serialize, state])

  return [state, setState]
}
```

### Notes

If you'd like to learn more about when different hooks are called and the order in which they're called, then open up `src/examples/hook-flow.png` and `src/examples/hook-flow.js`. Play around with that a bit and hopefully that will help solidify this for you. Note that understanding this isn't absolutely necessary for you to understand hooks, but it _will_ help you in some situations so it's useful to understand.

## c. `useState` : Tic-Tac-Toe game

#### Background

A `name` is one thing, but a real UI is a bit different. Often you need more than one element of state in your component, so you'll call `React.useState` more than once. Please note that each call to `React.useState` in a given component will give you a unique state and updater function.

### Exercise

We're going to build tic-tac-toe (with localStorage support)! If you've gone through React's official tutorial, this was lifted from that (except that example still uses classes).

You're going to need some managed state and some derived state:

-   **Managed State:** State that you need to explicitly manage
-   **Derived State:** State that you can calculate based on other state

`squares` is the managed state and it's the state of the board in a single-dimensional array:

```
[
  'X', 'O', 'X',
  'X', 'O', 'O',
  'X', 'X', 'O'
]
```

This will start out as an empty array because it's the start of the game.

`nextValue` will be either the string `X` or `O` and is derived state which you can determine based on the value of `squares`. We can determine whose turn it is based on how many "X" and "O" squares there are. We've written this out for you in a `calculateNextValue` function at the bottom of the file.

`winner` will be either the string `X` or `O` and is derived state which can also be determined based on the value of `squares` and we've provided a `calculateWinner` function you can use to get that value.

📜 Read more about derived state in [Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it)

### Alternate:

If you'd prefer to practice refactoring a class that does this to a hook, then you can open `src/exercise/04-classes.js` and open that on [an isolated page](http://localhost:3000/isolated/exercise/04-classes.js) to practice that.

### Extra Credit

#### 1. 💯 preserve state in `localStorage`

👨‍💼 Our customers want to be able to pause a game, close the tab, and then resume the game later. Can you store the game's state in `localStorage`?

#### 2. 💯 `useLocalStorageState`

It's cool that we can get localStorage support with a simple `useEffect`, but it'd be even cooler to use the `useLocalStorageState` hook that's already written for us in `src/utils.js`!

Refactor your code to use that custom hook instead. (This should be a pretty quick extra credit).

#### 3. 💯 add game history feature

Open `http://localhost:3000/isolated/final/04.extra-3.js` and see that the extra version supports keeping a history of the game and allows you to go backward and forward in time. See if you can implement that!

NOTE: This extra credit is one of the harder extra credits. Don't worry if you struggle on it!

💰 Tip, in the final example, we store the history of squares in an array of arrays. `[[/* step 0 squares */], [/* step 1 squares */], ...etc]`, so we have two states: `history` and `currentStep`.

💰 Tip, in the final example, we move the state management from the `Board` component to the `Game` component and that helps a bit. Here's what the JSX returned from the `Game` component is in the final version:

```javascript
return (
  <div className="game">
    <div className="game-board">
      <Board onClick={selectSquare} squares={currentSquares} />
      <button className="restart" onClick={restart}>
        restart
      </button>
    </div>
    <div className="game-info">
      <div>{status}</div>
      <ol>{moves}</ol>
    </div>
  </div>
)
```

**Solution**
```jsx
import * as React from 'react'

function Board({onClick, squares}) {
  function renderSquare(i) {
    return (
      <button className="square" onClick={() => onClick(i)}>
        {squares[i]}
      </button>
    )
  }

  return (
    <div>
      <div className="board-row">
        {renderSquare(0)}
        {renderSquare(1)}
        {renderSquare(2)}
      </div>
      <div className="board-row">
        {renderSquare(3)}
        {renderSquare(4)}
        {renderSquare(5)}
      </div>
      <div className="board-row">
        {renderSquare(6)}
        {renderSquare(7)}
        {renderSquare(8)}
      </div>
    </div>
  )
}

function Game() {
  const [currentStep, setCurrentStep] = React.useState(0)
  const [history, setHistory] = React.useState([Array(9).fill(null)])

  const currentSquares = history[currentStep]

  const nextValue = calculateNextValue(currentSquares)
  const winner = calculateWinner(currentSquares)
  const status = calculateStatus(winner, currentSquares, nextValue)

  React.useEffect(() => {
    window.localStorage.setItem('squares', JSON.stringify(currentSquares))
  })

  function selectSquare(square) {
    if (winner || currentSquares[square]) return
    const newHistory = history.slice(0, currentStep + 1)
    const squaresCopy = [...currentSquares]
    squaresCopy[square] = nextValue

    setHistory([...newHistory, squaresCopy])
    setCurrentStep(newHistory.length)
  }

  function restart() {
    setHistory([Array(9).fill(null)])
    setCurrentStep(0)
  }

  const moves = history.map((stepSquares, step) => {
    const description = step === 0 ? 'Go to Start' : `Go to move #${step}`
    const isCurrentStep = step === currentStep

    return (
      <li key={step}>
        <button disabled={isCurrentStep} onClick={() => setCurrentStep(step)}>
          {description} {isCurrentStep ? '(current)' : null}
        </button>
      </li>
    )
  })

  return (
    <div className="game">
      <div className="game-board">
        <Board onClick={selectSquare} squares={currentSquares} />
        <button className="restart" onClick={restart}>
          restart
        </button>
      </div>
      <div className="game-info">
        <div>{status}</div>
        <ol>{moves}</ol>
      </div>
    </div>
  )
}

// eslint-disable-next-line no-unused-vars
function calculateStatus(winner, squares, nextValue) {
  return winner
    ? `Winner: ${winner}`
    : squares.every(Boolean)
    ? `Scratch: Cat's game`
    : `Next player: ${nextValue}`
}

// eslint-disable-next-line no-unused-vars
function calculateNextValue(squares) {
  return squares.filter(Boolean).length % 2 === 0 ? 'X' : 'O'
}

// eslint-disable-next-line no-unused-vars
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ]
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i]
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a]
    }
  }
  return null
}

function App() {
  return <Game />
}

export default App
```

## d. `useRef` and `useEffect`: DOM interaction

#### Background

Often when working with React you'll need to integrate with UI libraries. Some of these need to work directly with the DOM. Remember that when you do: `<div>hi</div>` that's actually syntactic sugar for a `React.createElement` so you don't actually have access to DOM nodes in your function component. In fact, DOM nodes aren't created at all until the `ReactDOM.render` method is called. Your function component is really just responsible for creating and returning React Elements and has nothing to do with the DOM in particular.

So to get access to the DOM, you need to ask React to give you access to a particular DOM node when it renders your component. The way this happens is through a special prop called `ref`.

Here's a simple example of using the `ref` prop:

```javascript
function MyDiv() {
  const myDivRef = React.useRef()
  React.useEffect(() => {
    const myDiv = myDivRef.current
    // myDiv is the div DOM node!
    console.log(myDiv)
  }, [])
  return <div ref={myDivRef}>hi</div>
}
```

After the component has been rendered, it's considered "mounted." That's when the `React.useEffect` callback is called and so by that point, the ref should have its `current` property set to the DOM node. So often you'll do direct DOM interactions/manipulations in the `useEffect` callback.

### Exercise

In this exercise we're going to make a `<Tilt />` component that renders a div and uses the `vanilla-tilt` library to make it super fancy.

The thing is, `vanilla-tilt` works directly with DOM nodes to setup event handlers and stuff, so we need access to the DOM node. But because we're not the one calling `document.createElement` (React does) we need React to give it to us.

So in this exercise we're going to use a `ref` so React can give us the DOM node and then we can pass that on to `vanilla-tilt`.

Additionally, we'll need to clean up after ourselves if this component is unmounted. Otherwise we'll have event handlers dangling around on DOM nodes that are no longer in the document.

```jsx
import * as React from 'react'
import VanillaTilt from 'vanilla-tilt'

function Tilt({children}) {
  const tiltRef = React.useRef()

  React.useEffect(() => {
    const tiltNode = tiltRef.current
    VanillaTilt.init(tiltNode, {
      max: 25,
      speed: 400,
      glare: true,
      'max-glare': 0.5,
    })

    return function cleanUp() {
      tiltNode.vanillaTilt.destroy()
    }
  }, [])

  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}

function App() {
  return (
    <Tilt>
      <div className="totally-centered">vanilla-tilt.js</div>
    </Tilt>
  )
}

export default App
```

### Alternate:

If you'd prefer to practice refactoring a class that does this to a hook, then you can open `src/exercise/05-classes.js` and open that on [an isolated page](http://localhost:3000/isolated/exercise/05-classes.js) to practice that.

```jsx
import * as React from 'react'
import VanillaTilt from 'vanilla-tilt'

class Tilt extends React.Component {
  tiltRef = React.createRef()
  componentDidMount() {
    const tiltNode = this.tiltRef.current
    const vanillaTiltOptions = {
      max: 25,
      speed: 400,
      glare: true,
      'max-glare': 0.5,
    }
    VanillaTilt.init(tiltNode, vanillaTiltOptions)
  }
  componentWillUnmount() {
    this.tiltRef.current.vanillaTilt.destroy()
  }
  render() {
    return (
      <div ref={this.tiltRef} className="tilt-root">
        <div className="tilt-child">{this.props.children}</div>
      </div>
    )
  }
}
function App() {
  return (
    <Tilt>
      <div className="totally-centered">vanilla-tilt.js</div>
    </Tilt>
  )
}

export default App
```

## e. `useEffect`: HTTP requests
### Background

HTTP requests are another common side-effect that we need to do in applications. This is no different from the side-effects we need to apply to a rendered DOM or when interacting with browser APIs like `localStorage`. In all these cases, we do that within a `useEffect` hook callback. This hook allows us to ensure that whenever certain changes take place, we apply the side-effects based on those changes.

One important thing to note about the `useEffect` hook is that you cannot return anything other than the cleanup function. This has interesting implications with regard to async/await syntax:

```javascript
// this does not work, don't do this:
React.useEffect(async () => {
  const result = await doSomeAsyncThing()
  // do something with the result
})
```

The reason this doesn't work is because when you make a function async, it automatically returns a promise (whether you're not returning anything at all, or explicitly returning a function). This is due to the semantics of async/await syntax. So if you want to use async/await, the best way to do that is like so:

```javascript
React.useEffect(() => {
  async function effect() {
    const result = await doSomeAsyncThing()
    // do something with the result
  }
  effect()
})
```

This ensures that you don't return anything but a cleanup function.

🦉 I find that it's typically just easier to extract all the async code into a utility function which I call and then use the promise-based `.then` method instead of using async/await syntax:

```javascript
React.useEffect(() => {
  doSomeAsyncThing().then(result => {
    // do something with the result
  })
})
```

But how you prefer to do this is totally up to you :)

### Exercise

In this exercise, we'll be doing data fetching directly in a `useEffect` hook callback within our component.

Here we have a form where users can enter the name of a pokemon and fetch data about that pokemon. Your job will be to create a component which makes that fetch request. When the user submits a pokemon name, our `PokemonInfo` component will get re-rendered with the `pokemonName`

```jsx
function PokemonInfo({pokemonName}) {
  const [pokemon, setPokemon] = React.useState(null)
  // 🐨 Have state for the pokemon (null)
  // 🐨 use React.useEffect where the callback should be called whenever the
  // pokemon name changes.
  React.useEffect(() => {
    if (!pokemonName) return
    // Resetting the pokemon to null before fetching the new pokemon data
    setPokemon(null)
    fetchPokemon(pokemonName).then(pokemonData => {
      setPokemon(pokemonData)
    })
  }, [pokemonName])

  if (!pokemonName) {
    return 'Submit a pokemon'
  } else if (!pokemon) {
    return <PokemonInfoFallback name={pokemonName} />
  }
  return <PokemonDataView pokemon={pokemon} />
}
```

### Extra Credit

#### 1. 💯 handle errors

Unfortunately, sometimes things go wrong and we need to handle errors when they do so we can show the user useful information. Handle that error and render it out like so:

```jsx
<div role="alert">
  There was an error: <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
</div>
```

You can make an error happen by typing an incorrect pokemon name into the input.

One common question I get about this extra credit is how to handle promise errors. There are two ways to do it in this extra credit:

```javascript
// option 1: using .catch
fetchPokemon(pokemonName)
  .then(pokemon => setPokemon(pokemon))
  .catch(error => setError(error))

// option 2: using the second argument to .then
fetchPokemon(pokemonName).then(
  pokemon => setPokemon(pokemon),
  error => setError(error),
)
```

These are functionally equivalent for our purposes, but they are semantically different in general.

Using `.catch` means that you'll handle an error in the `fetchPokemon` promise, but you'll _also_ handle an error in the `setPokemon(pokemon)` call as well. This is due to the semantics of how promises work.

Using the second argument to `.then` means that you will catch an error that happens in `fetchPokemon` only. In this case, I knew that calling `setPokemon` would not throw an error (React handles errors and we have an API to catch those which we'll use later), so I decided to go with the second argument option.

However, in this situation, it doesn't really make much of a difference. If you want to go with the safe option, then opt for `.catch`.

```jsx
function PokemonInfo({pokemonName}) {
  const [pokemon, setPokemon] = React.useState(null)

  const [error, setError] = React.useState(null)

  // 🐨 Have state for the pokemon (null)
  // 🐨 use React.useEffect where the callback should be called whenever the
  // pokemon name changes.
  React.useEffect(() => {
    if (!pokemonName) return
    // Resetting the pokemon to null before fetching the new pokemon data
    setPokemon(null)
    setError(null)
    fetchPokemon(pokemonName).then(
      pokemonData => {
        return setPokemon(pokemonData)
      },
      error => {
        return setError(error)
      },
    )
  }, [pokemonName])

  if (error) {
    return (
      <div role="alert">
        There was an error:{' '}
        <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
      </div>
    )
  } else if (!pokemonName) {
    return 'Submit a pokemon'
  } else if (!pokemon) {
    return <PokemonInfoFallback name={pokemonName} />
  }
  return <PokemonDataView pokemon={pokemon} />
}
```

#### 2. 💯 use a status

Our logic for what to show the user when is kind of convoluted and requires that we be really careful about which state we set and when.

We could make things much simpler by having some state to set the explicit status of our component. Our component can be in the following "states":

-   `idle`: no request made yet
-   `pending`: request started
-   `resolved`: request successful
-   `rejected`: request failed

Try to use a status state by setting it to these string values rather than relying on existing state or booleans.

Learn more about this concept here: [Stop using `isLoading` booleans](https://kentcdodds.com/blog/stop-using-isloading-booleans)

💰 Warning: Make sure you call `setPokemon` before calling `setStatus`. We'll address that more in the next extra credit.

```jsx
function PokemonInfo({pokemonName}) {
  const [pokemon, setPokemon] = React.useState(null)

  const [error, setError] = React.useState(null)
  const [status, setStatus] = React.useState('idle')
  
  React.useEffect(() => {
    if (!pokemonName) return
    // Resetting the status to 'pending' before fetching the new pokemon data
    setStatus('pending')
    fetchPokemon(pokemonName).then(
      pokemonData => {
        setPokemon(pokemonData)
        setStatus('resolved') 
        // if status is updated before getting the pokemon data,
        // the image will not be fetched. Hence, in this case
        //  it is importednt to set the status after the image is fetched.
        // This issue will be fixed on next Extra Credit.
      },
      error => {
        setError(error)
        setStatus('rejected')
      },
    )
  }, [pokemonName])

  // App state using the status variable
  if (status === 'idle') {
    return 'Submit a pokemon'
  } else if (status === 'pending') {
    return <PokemonInfoFallback name={pokemonName} />
  } else if (status === 'rejected') {
    return (
      <div role="alert">
        There was an error:{' '}
        <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
      </div>
    )
  } else if (status === 'resolved') {
    return <PokemonDataView pokemon={pokemon} />
  }
  throw new Error('This would be impossible!')
}
```

#### 3. 💯 store the state in an object

You'll notice that we're calling a bunch of state updaters in a row. This is normally not a problem, but each call to our state updater can result in a re-render of our component. React normally batches these calls so you only get a single re-render, but it's unable to do this in an asynchronous callback (like our promise success and error handlers).

So you might notice that if you do this:

```javascript
setStatus('resolved')
setPokemon(pokemon)
```

You'll get an error indicating that you cannot read `image` of `null`. This is because the `setStatus` call results in a re-render that happens before the `setPokemon` happens.

> but it's unable to do this in an asynchronous callback

This is no longer the case in React 18 as it supports automatic batching for asynchronous callback too.

Learn more about this concept here: [New Feature: Automatic Batching](https://reactjs.org/blog/2022/03/29/react-v18.html#new-feature-automatic-batching)

Still it is better to maintain closely related states as an object rather than maintaining them using individual `useState` hooks.

Learn more about this concept here: [Should I useState or useReducer?](https://kentcdodds.com/blog/should-i-usestate-or-usereducer#conclusion)

In the future, you'll learn about how `useReducer` can solve this problem really elegantly, but we can still accomplish this by storing our state as an object that has all the properties of state we're managing.

See if you can figure out how to store all of your state in a single object with a single `React.useState` call so I can update my state like this:

```javascript
setState({status: 'resolved', pokemon})
```

```jsx
function PokemonInfo({pokemonName}) {
  const [state, setState] = React.useState({
    status: 'idle',
    pokemon: null,
    error: null,
  })

  const {status, error, pokemon} = state

  React.useEffect(() => {
    if (!pokemonName) return
    // Resetting the pokemon to null before fetching the new pokemon data
    setState({status: 'pending'})
    fetchPokemon(pokemonName).then(
      pokemon => {
        setState({pokemon, status: 'resolved'})
      },
      error => {
        setState({error, status: 'rejected'})
      },
    )
  }, [pokemonName])

  // App status using the status variable
  if (status === 'idle') {
    return 'Submit a pokemon'
  } else if (status === 'pending') {
    return <PokemonInfoFallback name={pokemonName} />
  } else if (status === 'rejected') {
    return (
      <div role="alert">
        There was an error:{' '}
        <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
      </div>
    )
  } else if (status === 'resolved') {
    return <PokemonDataView pokemon={pokemon} />
  }
  throw new Error('This would be impossible!')
}
```

#### 4. 💯 create an `ErrorBoundary` component

We've already solved the problem for errors in our request, we're only handling that one error. But there are a lot of different kinds of errors that can happen in our applications.

No matter how hard you try, eventually your app code just isn’t going to behave the way you expect it to and you’ll need to handle those exceptions. If an error is thrown and unhandled, your application will be removed from the page, leaving the user with a blank screen... Kind of awkward...

Luckily for us, there’s a simple way to handle errors in your application using a special kind of component called an [Error Boundary](https://reactjs.org/docs/error-boundaries.html). Unfortunately, there is currently no way to create an Error Boundary component with a function and you have to use a class component instead.

In this extra credit, read up on `ErrorBoundary` components, and try to create one that handles this and any other error for the `PokemonInfo` component.

💰 to make your error boundary component handle errors from the `PokemonInfo` component, instead of rendering the error within the `PokemonInfo` component, you'll need to `throw error` right in the function so React can hand that to the error boundary. So `if (status === 'rejected') throw error`.

```jsx
class ErrorBoundary extends React.Component {
  state = {error: null}

  static getDerivedStateFromError(error) {
    return {
      error,
    }
  }

  render() {
    const {error} = this.state
    if (error) {
      return <this.props.FallbackComponent error={error} />
    }
    return this.props.children
  }
}

function PokemonInfo({pokemonName}) {
  const [state, setState] = React.useState({
    status: 'idle',
    pokemon: null,
    error: null,
  })

  const {status, error, pokemon} = state

  React.useEffect(() => {
    if (!pokemonName) return
    // Resetting the pokemon to null before fetching the new pokemon data
    setState({status: 'pending'})
    fetchPokemon(pokemonName).then(
      pokemon => {
        setState({pokemon, status: 'resolved'})
      },
      error => {
        setState({error, status: 'rejected'})
      },
    )
  }, [pokemonName])

  // App status using the status variable
  if (status === 'idle') {
    return 'Submit a pokemon'
  } else if (status === 'pending') {
    return <PokemonInfoFallback name={pokemonName} />
  } else if (status === 'rejected') {
    throw error
  } else if (status === 'resolved') {
    return <PokemonDataView pokemon={pokemon} />
  }
  throw new Error('This would be impossible!')
}

function ErrorFallback({error}) {
  return (
    <div>
      There was an error:{' '}
      <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
    </div>
  )
}

function App() {
  const [pokemonName, setPokemonName] = React.useState('')

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
      <hr />
      <div className="pokemon-info">
        <ErrorBoundary FallbackComponent={ErrorFallback}>
          <PokemonInfo pokemonName={pokemonName} />
        </ErrorBoundary>
      </div>
    </div>
  )
}
```

#### 5. 💯 re-mount the error boundary

You might notice that with the changes we've added, we now cannot recover from an error. For example:

1.  Type an incorrect pokemon
2.  Notice the error
3.  Type a correct pokemon
4.  Notice it doesn't show that new pokemon's information

The reason this is happening is because the `error` that's stored in the internal state of the `ErrorBoundary` component isn't getting reset, so it's not rendering the `children` we're passing to it.

So what we need to do is reset the `ErrorBoundary`'s `error` state to `null` so it will re-render. But how do we access the internal state of our `ErrorBoundary` to reset it? Well, there are a few ways we could do this by modifying the `ErrorBoundary`, but one thing you can do when you want to _reset_ the state of a component, is by providing it a `key` prop which can be used to unmount and re-mount a component.

The `key` you can use? Try the `pokemonName`!

```jsx
function App() {
  const [pokemonName, setPokemonName] = React.useState('')

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
      <hr />
      <div className="pokemon-info">
	      {/* key prop is passed to ErrorBoundary */}
        <ErrorBoundary key={pokemonName} FallbackComponent={ErrorFallback}>
          <PokemonInfo pokemonName={pokemonName} />
        </ErrorBoundary>
      </div>
    </div>
  )
}
```

#### 6. 💯 use react-error-boundary

As cool as our own `ErrorBoundary` is, I'd rather not have to maintain it in the long-term. Luckily for us, there's an npm package we can use instead and it's already installed into this project. It's called [`react-error-boundary`](https://github.com/bvaughn/react-error-boundary).

Go ahead and give that a look and swap out our own `ErrorBoundary` for the one from `react-error-boundary`.

```jsx
import {ErrorBoundary} from 'react-error-boundary'
```

#### 7. 💯 reset the error boundary

You may have noticed a problem with the way we're resetting the internal state of the `ErrorBoundary` using the `key`. Unfortunately, we're not only re-mounting the `ErrorBoundary`, we're also re-mounting the `PokemonInfo` which results in a flash of the initial "Submit a pokemon" state whenever we change our pokemon.

So let's backtrack on that and instead we'll use `react-error-boundary`'s `resetErrorBoundary` function (which will be passed to our `ErrorFallback` component) to reset the state of the `ErrorBoundary` when the user clicks a "try again" button.

> 💰 feel free to open up the finished version by clicking the link in the app so you can get an idea of how this is supposed to work.

Once you have this button wired up, we need to react to this reset of the `ErrorBoundary`'s state by resetting our own state so we don't wind up triggering the error again. To do this we can use the `onReset` prop of the `ErrorBoundary`. In that function we can simply `setPokemonName` to an empty string.

```jsx
function ErrorFallback({error, resetErrorBoundary}) {
  return (
    <div>
      There was an error:{' '}
      <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
      <button onClick={resetErrorBoundary}>Try Again</button>
    </div>
  )
}

function App() {
  const [pokemonName, setPokemonName] = React.useState('')

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
  }

  function handleReset() {
    setPokemonName('')
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
      <hr />
      <div className="pokemon-info">
        <ErrorBoundary
          key={pokemonName}
          FallbackComponent={ErrorFallback}
          onReset={handleReset}
        >
          <PokemonInfo pokemonName={pokemonName} />
        </ErrorBoundary>
      </div>
    </div>
  )
}
```

#### 8. 💯 use `resetKeys`

Unfortunately now the user can't simply select a new pokemon and continue with their day. They have to first click "Try again" and then select their new pokemon. I think it would be cooler if they can just submit a new `pokemonName` and the `ErrorBoundary` would reset itself automatically.

Luckily for us `react-error-boundary` supports this with the `resetKeys` prop. You pass an array of values to `resetKeys` and if the `ErrorBoundary` is in an error state and any of those values change, it will reset the error boundary.

💰 Your `resetKeys` prop should be: `[pokemonName]`

```jsx
return (
    <div className="pokemon-info-app">
      <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
      <hr />
      <div className="pokemon-info">
        <ErrorBoundary
          key={pokemonName}
          FallbackComponent={ErrorFallback}
          onReset={handleReset}
          resetKeys={[pokemonName]} // ADDED THIS
        >
          <PokemonInfo pokemonName={pokemonName} />
        </ErrorBoundary>
      </div>
    </div>
  )
```

# Advanced React Hooks

## a. `useCallback`: custom hooks
### Background

React's `useState` hook can get you a really long way with React state management. That said, sometimes you want to separate the state logic from the components that make the state changes. In addition, if you have multiple elements of state that typically change together, then having an object that contains those elements of state can be quite helpful.

This is where `useReducer` comes in really handy. If you're familiar with redux, then you'll feel pretty comfortable here. If not, then you have less to unlearn 😉

This exercise will take you pretty deep into `useReducer`. Typically, you'll use `useReducer` with an object of state, but we're going to start by managing a single number (a `count`). We're doing this to ease you into `useReducer` and help you learn the difference between the convention and the actual API.

Here's an example of using `useReducer` to manage the value of a name in an input.

```javascript
function nameReducer(previousName, newName) {
  return newName
}

const initialNameValue = 'Joe'

function NameInput() {
  const [name, setName] = React.useReducer(nameReducer, initialNameValue)
  const handleChange = event => setName(event.target.value)
  return (
    <>
      <label>
        Name: <input defaultValue={name} onChange={handleChange} />
      </label>
      <div>You typed: {name}</div>
    </>
  )
}
```

One important thing to note here is that the reducer (called `nameReducer` above) is called with two arguments:

1.  the current state
2.  whatever it is that the dispatch function (called `setName` above) is called with. This is often called an "action."

### Exercise

We're going to start off as simple as possible with a `<Counter />` component. `useReducer` is absolutely overkill for a counter component like ours, but for now, just focus on making things work with `useReducer`.

```jsx
import * as React from 'react'

function countReducer(count, newCount) {
  return newCount
}

function Counter({initialCount = 0, step = 1}) {
  const [count, setCount] = React.useReducer(countReducer, initialCount)

  const increment = () => setCount(count + step)
  return <button onClick={increment}>{count}</button>
}

function App() {
  return <Counter />
}

export default App
```

📜 Here are two really helpful blog posts comparing `useState` and `useReducer`:

-   [Should I useState or useReducer?](https://kentcdodds.com/blog/should-i-usestate-or-usereducer)
-   [How to implement useState with useReducer](https://kentcdodds.com/blog/how-to-implement-usestate-with-usereducer)

### Extra Credit

#### 1. 💯 accept the step as the action

I want to change things a bit to have this API:

```javascript
const [count, changeCount] = React.useReducer(countReducer, initialCount)
const increment = () => changeCount(step)
```

How would you need to change your reducer to make this work?

This one is just to show that you can pass anything as the action.

```jsx
import * as React from 'react'

function countReducer(count, step) {
  return count + step
}

function Counter({initialCount = 0, step = 1}) {
  const [count, changeCount] = React.useReducer(countReducer, initialCount)

  const increment = () => changeCount(step)
  return <button onClick={increment}>{count}</button>
}

function App() {
  return <Counter />
}

export default App
```

#### 2. 💯 simulate `setState` with an object

Remember `this.setState` from class components? If not, lucky you 😉. Either way, let's see if you can figure out how to make the state updater (`dispatch` function) behave in a similar way by changing our `state` to an object (`{count: 0}`) and then calling the state updater with an object which merges with the current state.

So here's how I want things to look now:

```javascript
const [state, setState] = React.useReducer(countReducer, {
  count: initialCount,
})
const {count} = state
const increment = () => setState({count: count + step})
```

How would you need to change the reducer to make this work?

```jsx
const countReducer = (state, action) => ({...state, ...action})
```

#### 3. 💯 simulate `setState` with an object OR function

`this.setState` from class components can also accept a function. So let's add support for that with our simulated `setState` function. See if you can figure out how to make your reducer support both the object as in the last extra credit as well as a function callback:

```javascript
const [state, setState] = React.useReducer(countReducer, {
  count: initialCount,
})
const {count} = state
const increment = () =>
  setState(currentState => ({count: currentState.count + step}))
```

```jsx
const countReducer = (state, action) => ({
  ...state,
  ...(typeof action === 'function' ? action(state) : action),
})
```

#### 4. 💯 traditional dispatch object with a type and switch statement

Okay, now we can finally see what most people do conventionally (mostly thanks to redux). Update your reducer so I can do this:

```javascript
const [state, dispatch] = React.useReducer(countReducer, {
  count: initialCount,
})
const {count} = state
const increment = () => dispatch({type: 'INCREMENT', step})
```

```jsx
const countReducer = (state, action) => {
  const {type, step} = action
  const {count} = state
  switch (type) {
    case 'INCREMENT':
      return {count: count + step}
    default: {
      throw new Error(`Unsupported action type: ${type}`)
    }
  }
}
```

### 🦉 Other notes

#### lazy initialization

This one's not an extra credit, but _sometimes_ lazy initialization can be useful, so here's how we'd do that with our original hook App:

```javascript
function init(initialStateFromProps) {
  return {
    pokemon: null,
    loading: false,
    error: null,
  }
}

// ...

const [state, dispatch] = React.useReducer(reducer, props.initialState, init)
```

So, if you pass a third function argument to `useReducer`, it passes the second argument to that function and uses the return value for the initial state.

This could be useful if our `init` function read into localStorage or something else that we wouldn't want happening every re-render.

#### The full `useReducer` API

If you're into TypeScript, here's some type definitions for `useReducer`:

> Thanks to [Trey's blog post](https://levelup.gitconnected.com/db1858d1fb9c)

> Please don't spend too much time reading through this by the way!

```typescript
type Dispatch<A> = (value: A) => void
type Reducer<S, A> = (prevState: S, action: A) => S
type ReducerState<R extends Reducer<any, any>> = R extends Reducer<infer S, any>
  ? S
  : never
type ReducerAction<R extends Reducer<any, any>> = R extends Reducer<
  any,
  infer A
>
  ? A
  : never

function useReducer<R extends Reducer<any, any>, I>(
  reducer: R,
  initializerArg: I & ReducerState<R>,
  initializer: (arg: I & ReducerState<R>) => ReducerState<R>,
): [ReducerState<R>, Dispatch<ReducerAction<R>>]

function useReducer<R extends Reducer<any, any>, I>(
  reducer: R,
  initializerArg: I,
  initializer: (arg: I) => ReducerState<R>,
): [ReducerState<R>, Dispatch<ReducerAction<R>>]

function useReducer<R extends Reducer<any, any>>(
  reducer: R,
  initialState: ReducerState<R>,
  initializer?: undefined,
): [ReducerState<R>, Dispatch<ReducerAction<R>>]
```

`useReducer` is pretty versatile. The key takeaway here is that while conventions are useful, understanding the API and its capabilities is more important.

## b. `useCallback`: custom hooks

### Background

#### Memoization in general

Memoization: a performance optimization technique which eliminates the need to recompute a value for a given input by storing the original computation and returning that stored value when the same input is provided. Memoization is a form of caching. Here's a simple implementation of memoization:

```typescript
const values = {}
function addOne(num: number) {
  if (values[num] === undefined) {
    values[num] = num + 1 // <-- here's the computation
  }
  return values[num]
}
```

One other aspect of memoization is value referential equality. For example:

```typescript
const dog1 = new Dog('sam')
const dog2 = new Dog('sam')
console.log(dog1 === dog2) // false
```

Even though those two dogs have the same name, they are not the same. However, we can use memoization to get the same dog:

```typescript
const dogs = {}
function getDog(name: string) {
  if (dogs[name] === undefined) {
    dogs[name] = new Dog(name)
  }
  return dogs[name]
}

const dog1 = getDog('sam')
const dog2 = getDog('sam')
console.log(dog1 === dog2) // true
```

You might have noticed that our memoization examples look very similar. Memoization is something you can implement as a generic abstraction:

```typescript
function memoize<ArgType, ReturnValue>(cb: (arg: ArgType) => ReturnValue) {
  const cache: Record<ArgType, ReturnValue> = {}
  return function memoized(arg: ArgType) {
    if (cache[arg] === undefined) {
      cache[arg] = cb(arg)
    }
    return cache[arg]
  }
}

const addOne = memoize((num: number) => num + 1)
const getDog = memoize((name: string) => new Dog(name))
```

Our abstraction only supports one argument, if you want to make it work for any type/number of arguments, knock yourself out.

#### Memoization in React

Luckily, in React we don't have to implement a memoization abstraction. They made two for us! `useMemo` and `useCallback`. For more on this read: [Memoization and React](https://epicreact.dev/memoization-and-react).

You know the dependency list of `useEffect`? Here's a quick refresher:

```javascript
React.useEffect(() => {
  window.localStorage.setItem('count', count)
}, [count]) // <-- that's the dependency list
```

Remember that the dependency list is how React knows whether to call your callback (and if you don't provide one then React will call your callback every render). It does this to ensure that the side effect you're performing in the callback doesn't get out of sync with the state of the application.

But what happens if I use a function in my callback?

```javascript
const updateLocalStorage = () => window.localStorage.setItem('count', count)
React.useEffect(() => {
  updateLocalStorage()
}, []) // <-- what goes in that dependency list?
```

We could just put the `count` in the dependency list and that would actually/accidentally work, but what would happen if one day someone were to change `updateLocalStorage`?

```diff
- const updateLocalStorage = () => window.localStorage.setItem('count', count)
+ const updateLocalStorage = () => window.localStorage.setItem(key, count)
```

Would we remember to update the dependency list to include the `key`? Hopefully we would. But this can be a pain to keep track of dependencies. Especially if the function that we're using in our `useEffect` callback is coming to us from props (in the case of a custom component) or arguments (in the case of a custom hook).

Instead, it would be much easier if we could just put the function itself in the dependency list:

```javascript
const updateLocalStorage = () => window.localStorage.setItem('count', count)
React.useEffect(() => {
  updateLocalStorage()
}, [updateLocalStorage]) // <-- function as a dependency
```

The problem with that it will trigger the `useEffect` to run every render. This is because `updateLocalStorage` is defined inside the component function body. So it's re-initialized every render. Which means it's brand new every render. Which means it changes every render. Which means... you guessed it, our `useEffect` callback will be called every render!

**This is the problem `useCallback` solves**. And here's how you solve it

```javascript
const updateLocalStorage = React.useCallback(
  () => window.localStorage.setItem('count', count),
  [count], // <-- yup! That's a dependency list!
)
React.useEffect(() => {
  updateLocalStorage()
}, [updateLocalStorage])
```

What that does is we pass React a function and React gives that same function back to us... Sounds kinda useless right? Imagine:

```javascript
// this is not how React actually implements this function. We're just imagining!
function useCallback(callback) {
  return callback
}
```

Uhhh... But there's a catch! On subsequent renders, if the elements in the dependency list are unchanged, instead of giving the same function back that we give to it, React will give us the same function it gave us last time. So imagine:

```javascript
// this is not how React actually implements this function. We're just imagining!
let lastCallback
function useCallback(callback, deps) {
  if (depsChanged(deps)) {
    lastCallback = callback
    return callback
  } else {
    return lastCallback
  }
}
```

So while we still create a new function every render (to pass to `useCallback`), React only gives us the new one if the dependency list changes.

In this exercise, we're going to be using `useCallback`, but `useCallback` is just a shortcut to using `useMemo` for functions:

```typescript
// the useMemo version:
const updateLocalStorage = React.useMemo(
  // useCallback saves us from this annoying double-arrow function thing:
  () => () => window.localStorage.setItem('count', count),
  [count],
)

// the useCallback version
const updateLocalStorage = React.useCallback(
  () => window.localStorage.setItem('count', count),
  [count],
)
```

🦉 A common question with this is: "Why don't we just wrap every function in `useCallback`?" You can read about this in my blog post [When to useMemo and useCallback](https://kentcdodds.com/blog/usememo-and-usecallback).

🦉 And if the concept of a "closure" is new or confusing to you, then [give this a read](https://mdn.io/closure). (Closures are one of the reasons it's important to keep dependency lists correct.)

### Exercise

**People tend to find this exercise more difficult,** so I strongly advise spending some time understanding how the code works before making any changes!

Also, one thing to keep in mind is that React hooks are a great foundation upon which many have been built. For that reason, you don't often need to go this deep into making custom hooks. So if you find this one isn't clicking for you, know that you _are_ learning and when you _do_ face a situation when you need to use this knowledge, you'll be able to come back and it will click right into place.

👨‍💼 Peter the Product Manager told us that we've got more features coming our way that will require managing async state. We've already got some code for our pokemon lookup feature (if you've gone through the "React Hooks" workshop already, then this should be familiar, if not, spend some time playing with the app to get up to speed with what we're dealing with here). We're going to refactor out the async logic so we can reuse this in other areas of the app.

**So, your job is** to extract the logic from the `PokemonInfo` component into a custom and generic `useAsync` hook. In the process you'll find you need to do some fancy things with dependencies (dependency arrays are the biggest challenge to deal with when making custom hooks).

NOTE: In this part of the exercise, we don't need `useCallback`. We'll add it in the extra credits. It's important that you work on this refactor first so you can appreciate the value `useCallback` provides in certain circumstances.

### Extra Credit

#### 1. 💯 use `useCallback` to empower the user to customize memoization

Unfortunately, the ESLint plugin is unable to determine whether the `dependencies` argument is a valid argument for `useEffect` which is a shame, and normally I'd say just ignore it and move on. But, there's another solution to this problem which I think is probably better.

Instead of accepting `dependencies` to `useAsync`, why don't we just treat the `asyncCallback` as a dependency? Any time `asyncCallback` changes, we know that we should call it again. The problem is that because our `asyncCallback` depends on the `pokemonName` which comes from props, it has to be defined within the body of the component, which means that it will be defined on every render which means it will be new every render. This is where `React.useCallback` comes in!

Here's another example of the `React.useCallback` API:

```javascript
function ConsoleGreeting(props) {
  const greet = React.useCallback(
    greeting => console.log(`${greeting} ${props.name}`),
    [props.name],
  )

  React.useEffect(() => {
    const helloGreeting = 'Hello'
    greet(helloGreeting)
  }, [greet])
  return <div>check the console</div>
}
```

The first argument to `useCallback` is the callback you want called, the second argument is an array of dependencies which is similar to `useEffect`. When one of the dependencies changes between renders, the callback you passed in the first argument will be the one returned from `useCallback`. If they do not change, then you'll get the callback which was returned the previous time (so the callback remains the same between renders).

So we only want our `asyncCallback` to change when the `pokemonName` changes. See if you can make things work like this:

```javascript
// 🐨 you'll need to wrap asyncCallback in React.useCallback
function asyncCallback() {
  if (!pokemonName) {
    return
  }
  return fetchPokemon(pokemonName)
}

// 🐨 you'll need to update useAsync to remove the dependencies and list the
// async callback as a dependency.
const state = useAsync(asyncCallback)
```

#### 2. 💯 return a memoized `run` function from `useAsync`

Requiring users to provide a memoized value is fine. You can document it as part of the API and expect people to just read the docs right? lol, that's hilarious 😂 It'd be WAY better if we could redesign the API a bit so we (as the hook developers) are the ones who have to memoize the function, and the users of our hook don't have to worry about it.

So see if you can redesign this a little bit by providing a (memoized) `run` function that people can call in their own `useEffect` like this:

```javascript
// 💰 destructuring this here now because it just felt weird to call this
// "state" still when it's also returning a function called "run" 🙃
const {data: pokemon, status, error, run} = useAsync({ status: pokemonName ? 'pending' : 'idle' })

React.useEffect(() => {
  if (!pokemonName) {
    return
  }
  // 💰 note the absence of `await` here. We're literally passing the promise
  // to `run` so `useAsync` can attach it's own `.then` handler on it to keep
  // track of the state of the promise.
  const pokemonPromise = fetchPokemon(pokemonName)
  run(pokemonPromise)
}, [pokemonName, run])
```

#### 3. 💯 make `safeDispatch` with `useCallback`, `useRef`, and `useEffect`

**NOTICE: Things have changed slightly.** The app you're running the exercises in was changed since the videos were recorded and you can no longer see this issue by changing the exercise. All the exercises are now rendered in an iframe on the exercise pages, so when you go to a different exercise, you're effectively "closing" the page, so all JS execution for that exercise stops.

So I've added a little checkbox which you can use to mount and unmount the component with ease. This has the benefit of also working on the isolated page as well. On the exercise page, you'll want to make sure that your console output is showing the output from the iframe by [selecting the right context](https://developers.google.com/web/tools/chrome-devtools/console/reference#context).

I've also added a test for this one to help make sure you've got it right.

Also notice that while what we're doing here is still useful and you'll learn valuable skills, the warning we're suppressing [goes away in React v18](https://github.com/reactwg/react-18/discussions/82).

Phew, ok, back to your extra credit!

This one's a bit tricky, and I'm going to be intentionally vague here to give you a bit of a challenge, but consider the scenario where we fetch a pokemon, and before the request finishes, we change our mind and navigate to a different page (or uncheck the mount checkbox). In that case, the component would get removed from the page ("unmounted") and when the request finally does complete, it will call `dispatch`, but because the component has been removed from the page, we'll get this warning from React:

```text
Warning: Can't perform a React state update on an unmounted component. This is a no-op, but it indicates a memory leak in your application. To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
```

The best solution to this problem would be to [cancel the request](https://developers.google.com/web/updates/2017/09/abortable-fetch), but even then, we'd have to handle the error and prevent the `dispatch` from being called for the rejected promise.

So see whether you can work out a solution for preventing `dispatch` from being called if the component is unmounted. Depending on how you implement this, you might need `useRef`, `useCallback`, and `useEffect`.

### 🦉 Other notes

#### `useEffect` and `useCallback`

The use case for `useCallback` in the exercise is a perfect example of the types of problems `useCallback` is intended to solve. However the examples in these instructions are intentionally contrived. You can simplify things a great deal by _not_ extracting code from `useEffect` into functions that you then have to memoize with `useCallback`. Read more about this here: [Myths about useEffect](https://epicreact.dev/myths-about-useeffect).

#### `useCallback` use cases

The entire purpose of `useCallback` is to memoize a callback for use in dependency lists and props on memoized components (via `React.memo`, which you can learn more about from the performance workshop). The _only_ time it's useful to use `useCallback` is when the function you're memoizing is used in one of those two situations.