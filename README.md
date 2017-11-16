# React Code Review Checklist
An opinionated code-review checklist for React applications.

## Keep code DRY (Don't repeat yourself)

## If a variable reaches three degress depth or more, destructure it.
```javascript
const {value} = this.props
const {myVariable} = data.person
```

## No other logic aside from display logic inside components

## No logic inside Reducers

### Put your other logic inside Action Creators

## Enforce propTypes (Use ES7 Property Initializers)
Your proptypes act as a dictionary on what the expected props should be. This enable developers to understand your code faster and ensures the integrity of the props.
```javascript
class MyComponent extends Component {
    static propTypes = {
        model: Proptypes.string
        ...
    }
}
```

## Use ES 7 Property Initializers for declaring state and default props
Property initializers reduces the amount of overhead a developer has to code in order to start making a component.
It get rids of the need of a constructor, or binding your components inside the constructor.
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

### Use shape for propTypes wherever applicable
Because our proptypes act as a our guide/dictionary to a component, a detailed view on what the props should contain is also needed.
```javascript
MyComponent.propTypes = {
    optionalObjectWithShape: PropTypes.shape({
        color: PropTypes.string,
        fontSize: PropTypes.number
    }),
}
```

## Destructure props and state as individual constants
```javascript
const {visible, marker} = this.state
const {data, config} = this.props
```

## No commented code

## Keep components small

## Event listeners removed
Creating anything that has the ability to manipulate the DOM directly is not React-friendly. React relies on its virtual dom to render objects.
Directly changing the DOM will blind the virtual DOM from those changes.
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
While this not really that useful for direct state setting, this is useful if the developer is basing the new value of the state from its previous value.
This will ensure that the setting of the new state is done after any potential changes in the state.
```javascript
this.setState(prevState => ({visible: !prevState.visible}));
```

## JSX markup should be no more than 50 lines

## Stateless components for components that don't use state

## Naming conventions followed for variables, file names, translations

## No unused variables and functions/methods

## Removed unused packages from NPM

## No api calls in containers, delegate to Stores

## Use Link element instead of Anchor element
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
Using fat arrow functions will bind the "this" keyword in the function. Meaning, "this" will always refer to the component, and not to "null" or "undefined"
```javascript
const myFunction = () => {
    this.myObject // 'this' is defined here since we are using fat arrow for function creation
}
```

## No new closures passed to subcomponents
Example: https://jsfiddle.net/johnnyji/mtkjc5on/
Ref: http://johnnyji.me/react/2016/06/27/why-arrow-functions-murder-react-performance.html
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
First, this will make the javascript code more optimized as the translator will have faster reading times because of the consts and let restrictions.
Second, this will make error detection easier as developers can keep track if a variable that should not change its value, changes its value.
Third, the programming pattern develop when using these two is cleaner compared to using var.
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
This is in connection with using ES7 Property Initializers
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


