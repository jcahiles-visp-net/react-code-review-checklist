# react-code-review-checklist
An opinionated code-review checklist for React applications.

## Keep code DRY (Don't repeat yourself)

## Enforce propTypes (Use ES7 Property Initializers)
```javascript
class MyComponent extends Component {
    static propTypes = {
        model: Proptypes.string
        ...
    }
}
```

## Use ES 7 Property Initializers for declaring state and default props
```javascript
class MyComponent extends Component {
    state = {visible: true}

    static propTypes = {
        model: Proptypes.string
        ...
    }

    static defaultProps = {
        model: {title: 'VISP'},
        ...
    }

}
```

## Use shape for propTypes wherever applicable

## Destructure props and state as individual constants
```javascript
const {visible, marker} = this.state
const {data, config} = this.props
```

## No commented code

## Keep components small

## Event listeners removed
```javascript
// Don't do this inside a react component
const value = document.getElementById('check').addEventListener('click', function(){
    ...
})

// Make use of the event props
const handleClick = (event) => {
    event.preventDefault()
}

<MyComponent onClick={this.handleClick} >
```

## setState callback function is used
```javascript
this.setState(prevState => ({visible: !prevState.visible}));
```

## JSX markup should be no more than 50 lines

## Stateless components for components that don't use state

## Naming conventions followed for variables, file names, translations

## No unused variables and functions/methods

## Removed unused packages from NPM

## No api calls in containers, delegate to Stores

## Use '<Link />' instead of '<a />'
```javascript
// If using react-router, use its Link component
import {Link} from 'react-router-dom'   // react-router 4.x
import {Link} from 'react-router'       //react-router 3.x, 2.x, 1.x

...
render = () => {
    return (
        <div>
            <Link>This is a link</Link>
        </div>
    )
}
...
```

## No unused props are being passed

## Should have descriptive comments to functions/code, even one liner 

## Store mock data for unit tests, avoid cluttering of mock code

## Create mock data using loops, for easy maintainability 

## No state updates in loop

## Move data to constants if used in multiple files, like statusText and status code

## Use fat arrow instead of var that = this
```javascript
const myFunction = () => {
    this.myObject // 'this' is defined here since we are using fat arrow for function creation
}
```

## No new closures passed to subcomponents
```javascript
<input
    type="text"
    value={model.name}
    // onChange={(e) => { model.name = e.target.value }}
    // ^ Not this. Use the below:
    onChange={this.handleChange}
    placeholder="Your Name"
/>
```

## Use let/const over var
```javascript
// Don't use this
var visible = false;

// Use this instead
const name = 'VISP'     // If value of variable will not change during runtime
let visible = false     // If value of variable is expected to change during runtime
```

## No nested ternaries, specially inside 'render' function
```javascript
...
{
    // Don't do this
    this.state.visible
    ? return false
    : this.state.model === 'check'
        ?   return false
        : this.state.arrow > 20
            ?   return false
            :   return true
}
...
// If instant conditionals needed, use IIFE. Better solution would be to make a new class function
{() => {
    if(this.state.visible){
        return false
    } else {
        if(this.state.model === 'check'){
            return false
        } else {
            if(this.state.arrow > 20){
                return false
            } else {
                return true
            }
        }
    }
}}
```

## Use '' in JS code and "" in JSX

## No useless constructor
```javascript
// This is an ES 6 implementation
class MyComponent extends Component {
    constructor(props){
        this.state = {
            ...
        }
    }
}

// This is an ES 7 implementation
class MyComponent extends Component {
    state = {
        ...
    }
}
```


