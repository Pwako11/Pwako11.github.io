---
layout: post
title:      "Lifecycle methods in React components"
date:       2021-08-10 10:03:52 +0000
permalink:  Lifecycle_in_React_component
---

# Lifecycle Methods
React lets you define components as classes or functions. Components defined as classes provide more features. Some of these features inlcude methods that are a hook into the lifecycle of a react component. they can be used in ES6 class components, but not in functional stateless components. Each component has several “lifecycle methods” that you can override to run code at particular times in the process. The lifecyle methods are categorized in three main processes: `Mounting`, `Updating` and `Unmounting`.   

## Mounting 
During the `Mounting` process, an instance of the component is created and insterted in the DOM. The methods in this process are called in a specific order:
#### `constructor(`)
#### `componentWillMount()`
#### `render()`
#### `componentDidMount()`
The `constructor()` is called first, `componentWillMount()` gets called before the `render()` method and `componentDidMount()` is called after the render method. 
 
## Updating 
During the `Update` process the methods in this lifecycle are called when the state or the props in a component change. the methods in this process are called in the following order:
#### `static getDerivedStateFromProps()`
#### `shouldComponentUpdate()`
#### `render(`)
#### `componentDidUpdate()`
`render()` lifecycle method is mandatory and returns the elements as an output of teh component. This lifecycle event gets and input as props and state and returns an element. `shouldComponentUpdate()` is called when component updates due to state changes. `componentDidUpdate()` is used to perform further asynchronous requests.   

## Unmounting. 
Unmounting lifecycle, has only one lifecycle method: `componentWillUnmount()`. This method is called before your component is destroyed. This method is used to component clean up tasks. 

# Adding Lifecycle Methods to a Class

In complex/manture React applications with many components, it is very important to optimize your applications performance by freeing up resources taken by components when they are destroyed. 

In this example we will look will `mount` a clock and `unmount` the clock as we clear the timer. 

here we are declaring special methods on the component class to run some code when a component mounts and unmounts:

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```



The `componentDidMount()`method runs after the component output has been rendered to the DOM. This is a good place to set up a timer:

```
componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

While this.props is set up by React itself and this.state has a special meaning, you are free to add additional fields to the class manually if you need to store something that doesn’t participate in the data flow (like a timer ID).

We will tear down the timer in the componentWillUnmount() lifecycle method:

```
componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

Finally, we will implement a method called tick() that the Clock component will run every second.

It will use this.setState() to schedule updates to the component local state:

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```