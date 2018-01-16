# React

title	category	layout	ads	tags	updated	weight	keywords	intro
React.js
React
2017/sheet
true
Featured
2017-10-10
-10
React.Component
render()
componentDidMount()
props/state
dangerouslySetInnerHTML
[React](https://reactjs.org/) is a JavaScript library for building user interfaces. This guide targets React v15 to v16.
{%raw%}

Components

{: .-three-column}

Components

{: .-prime}

import React from 'react'
import ReactDOM from 'react-dom'
{: .-setup}

class Hello extends React.Component {
  render () {
    return <div className='message-box'>
      Hello {this.props.name}
    </div>
  }
}
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
Use the React.js jsfiddle to start hacking. (or the unofficial jsbin)

Properties

<Video fullscreen={true} />
{: .-setup}

render () {
  this.props.fullscreen
  ···
}
{: data-line="2"}

Use this.props to access properties passed to the component.

See: Properties

States

constructor(props) {
  super(props)
  this.state = {}
}
this.setState({ username: 'rstacruz' })
render () {
  this.state.username
  ···
}
{: data-line="2"}

Use states (this.state) to manage dynamic data.

See: States

Nesting

class Info extends React.Component {
  render () {
    const { avatar, username } = this.props

    return <div>
      <UserAvatar src={avatar} />
      <UserProfile username={username} />
    </div>
  }
}
{: data-line="6,7"}

Nest components to separate concerns.

See: Composing Components

Children

<AlertBox>
  <h1>You have pending notifications</h1>
</AlertBox>
{: data-line="2"}

class AlertBox extends React.Component {
  render () {
    return <div className='alert-box'>
      {this.props.children}
    </div>
  }
}
{: data-line="4"}

Children are passed as the children property.

Defaults

Setting default props

Hello.defaultProps = {
  color: 'blue'
}
{: data-line="1"}

See: defaultProps

Setting default state

class Hello extends React.Component {
  constructor (props) {
    super(props)
    this.state = { visible: true }
  }
}
{: data-line="4"}

Set the default state in the constructor().

See: Setting the default state

Other components

{: .-three-column}

Function components

function MyComponent ({ name }) {
  return <div className='message-box'>
    Hello {name}
  </div>
}
{: data-line="1"}

Functional components have no state. Also, their props are passed as the first parameter to a function.

See: Function and Class Components

Pure components

class MessageBox extends React.PureComponent {
  ···
}
{: data-line="1"}

Performance-optimized version of React.Component. Doesn't rerender if props/state hasn't changed.

See: Pure components

Component API

this.forceUpdate()
this.setState({ ... })
this.state
this.props
These methods and properties are available for Component instances.

See: Component API

Lifecycle

{: .-two-column}

Mounting

Method	Description
constructor (props)	Before rendering #
componentWillMount()	Don't use this #
render()	Render #
componentDidMount()	After rendering (DOM available) #
---	---
componentWillUnmount()	Before DOM removal #
---	---
componentDidCatch()	Catch errors (16+) #
Set initial the state on constructor(). Add DOM event handlers, timers (etc) on componentDidMount(), then remove them on componentWillUnmount().

Updating

Method	Description
componentWillReceiveProps (newProps)	Use setState() here
shouldComponentUpdate (newProps, newState)	Skips render() if returns false
componentWillUpdate (newProps, newState)	Can't use setState() here
render()	Render
componentDidUpdate (prevProps, prevState)	Operate on the DOM here
Called when parents change properties and .setState(). These are not called for initial renders.

See: Component specs

DOM nodes

{: .-two-column}

References

class MyComponent extends React.Component {
  render () {
    return <div>
      <input ref={el => this.input = el} />
    </div>
  }

  componentDidMount () {
    this.input.focus()
  }
}
{: data-line="4,9"}

Allows access to DOM nodes.

See: Refs and the DOM

DOM Events

class MyComponent extends React.Component {
  render () {
    <input type="text"
        value={this.state.value}
        onChange={event => this.onChange(event)} />
  }

  onChange (event) {
    this.setState({ value: event.target.value })
  }
}
{: data-line="5,9"}

Pass functions to attributes like onChange.

See: Events

Other features

Transferring props

<VideoPlayer src="video.mp4" />
{: .-setup}

class VideoPlayer extends React.Component {
  render () {
    return <VideoEmbed {...this.props} />
  }
}
{: data-line="3"}

Propagates src="..." down to the sub-component.

See Transferring props

Top-level API

React.createClass({ ... })
React.isValidElement(c)
ReactDOM.render(<Component />, domnode, [callback])
ReactDOM.unmountComponentAtNode(domnode)
ReactDOMServer.renderToString(<Component />)
ReactDOMServer.renderToStaticMarkup(<Component />)
There are more, but these are most common.

See: React top-level API

JSX patterns

{: .-two-column}

Style shorthand

var style = { height: 10 }
return <div style={style}></div>
return <div style={{ margin: 0, padding: 0 }}></div>
See: Inline styles

Inner HTML

function markdownify() { return "<p>...</p>"; }
<div dangerouslySetInnerHTML={{__html: markdownify()}} />
See: Dangerously set innerHTML

Lists

class TodoList extends React.Component {
  render () {
    const { items } = this.props

    return <ul>
      {items.map(item =>
        <TodoItem item={item} key={item.key} />)}
    </ul>
  }
}
{: data-line="6,7"}

Always supply a key property.

Conditionals

<div>
  {showMyComponent
    ? <MyComponent />
    : <OtherComponent />}
</div>
Short-circuit evaluation

<div>
  {showPopup && <Popup />}
</div>
New features

{: .-three-column}

Returning fragments

render () {
  // Don't forget the keys!
  return [
    <li key="A">First item</li>,
    <li key="B">Second item</li>
  ]
}
{: data-line="3,4,5,6"}

You can return multiple nodes as arrays.

See: Fragments and strings

Returning strings

render() {
  return 'Look ma, no spans!';
}
{: data-line="2"}

You can return just a string.

See: Fragments and strings

Errors

class MyComponent extends React.Component {
  ···
  componentDidCatch (error, info) {
    this.setState({ error })
  }
}
{: data-line="3,4,5"}

Catch errors via componentDidCatch. (React 16+)

See: Error handling in React 16

Portals

render () {
  return React.createPortal(
    this.props.children,
    document.getElementById('menu')
  )
}
{: data-line="2,3,4,5"}

This renders this.props.children into any location in the DOM.

See: Portals

Hydration

const el = document.getElementById('app')
ReactDOM.hydrate(<App />, el)
{: data-line="2"}

Use ReactDOM.hydrate instead of using ReactDOM.render if you're rendering over the output of ReactDOMServer.

See: Hydrate

Property validation

{: .-three-column}

PropTypes

import PropTypes from 'prop-types'
{: .-setup}

See: Typechecking with PropTypes

| any | Anything |

Basic

| string | | | number | | | func | Function | | bool | True or false |

Enum

| oneOf(any) | Enum types | | oneOfType(type array) | Union |

Array

| array | | | arrayOf(...) | |

Object

| object | | | objectOf(...) | Object with values of a certain type | | instanceOf(...) | Instance of a class | | shape(...) | |

Elements

| element | React element | | node | DOM node |

Required

| (···).isRequired | Required |

Basic types

MyComponent.propTypes = {
  email:      PropTypes.string,
  seats:      PropTypes.number,
  callback:   PropTypes.func,
  isClosed:   PropTypes.bool,
  any:        PropTypes.any
}
Required types

MyCo.propTypes = {
  name:  PropTypes.string.isRequired
}
Elements

MyCo.propTypes = {
  // React element
  element: PropTypes.element,

  // num, string, element, or an array of those
  node: PropTypes.node
}
Enumerables (oneOf)

MyCo.propTypes = {
  direction: PropTypes.oneOf([
    'left', 'right'
  ])
}
Arrays and objects

MyCo.propTypes = {
  list: PropTypes.array,
  ages: PropTypes.arrayOf(PropTypes.number),
  user: PropTypes.object,
  user: PropTypes.objectOf(PropTypes.number),
  message: PropTypes.instanceOf(Message)
}
MyCo.propTypes = {
  user: PropTypes.shape({
    name: PropTypes.string,
    age:  PropTypes.number
  })
}
Use .array[Of], .object[Of], .instanceOf, .shape.

Custom validation

MyCo.propTypes = {
  customProp: (props, key, componentName) => {
    if (!/matchme/.test(props[key])) {
      return new Error('Validation failed!')
    }
  }
}
Also see

React website (reactjs.org)
React cheatsheet (reactcheatsheet.com)
Awesome React (github.com)
React v0.14 cheatsheet Legacy version
{%endraw%}
