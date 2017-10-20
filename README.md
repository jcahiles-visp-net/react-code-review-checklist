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

## Use '' in JS code and "" in JSX

## No useless constructor


