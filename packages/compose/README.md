# Compose

The `compose` package is a collection of handy [Hooks](https://reactjs.org/docs/hooks-intro.html) and [Higher Order Components](https://facebook.github.io/react/docs/higher-order-components.html) (HOCs) you can use to wrap your WordPress components and provide some basic features like: state, instance id, pure...

The `compose` function is an alias to [flowRight](https://lodash.com/docs/#flowRight) from Lodash. It comes from functional programming, and allows you to compose any number of functions. You might also think of this as layering functions; `compose` will execute the last function first, then sequentially move back through the previous functions passing the result of each function upward.

An example that illustrates it for two functions:

```js
const compose = ( f, g ) => x
    => f( g( x ) );
```

Here's a simplified example of **compose** in use from Gutenberg's [`PluginSidebar` component](https://github.com/WordPress/gutenberg/blob/master/packages/edit-post/src/components/sidebar/plugin-sidebar/index.js):

Using compose:

```js
const applyWithSelect = withSelect( ( select, ownProps ) => {
	return doSomething( select, ownProps);
} );
const applyWithDispatch = withDispatch( ( dispatch, ownProps ) => {
	return doSomethingElse( dispatch, ownProps );
} );

export default compose(
	withPluginContext,
	applyWithSelect,
	applyWithDispatch,
)( PluginSidebarMoreMenuItem );
```

Without `compose`, the code would look like this:

```js
const applyWithSelect = withSelect( ( select, ownProps ) => {
	return doSomething( select, ownProps);
} );
const applyWithDispatch = withDispatch( ( dispatch, ownProps ) => {
	return doSomethingElse( dispatch, ownProps );
} );

export default withPluginContext(
	applyWithSelect(
		applyWithDispatch(
			PluginSidebarMoreMenuItem
		)
	)
);
```

## Installation

Install the module

```bash
npm install @wordpress/compose --save
```

_This package assumes that your code will run in an **ES2015+** environment. If you're using an environment that has limited or no support for ES2015+ such as lower versions of IE then using [core-js](https://github.com/zloirock/core-js) or [@babel/polyfill](https://babeljs.io/docs/en/next/babel-polyfill) will add support for these methods. Learn more about it in [Babel docs](https://babeljs.io/docs/en/next/caveats)._

## API

For more details, you can refer to each Higher Order Component's README file. [Available components are located here.](https://github.com/WordPress/gutenberg/tree/master/packages/compose/src)

<!-- START TOKEN(Autogenerated API docs) -->

<a name="compose" href="#compose">#</a> **compose**

Composes multiple higher-order components into a single higher-order component. Performs right-to-left function
composition, where each successive invocation is supplied the return value of the previous.

_Parameters_

-   _hocs_ `...Function`: The HOC functions to invoke.

_Returns_

-   `Function`: Returns the new composite function.

<a name="createHigherOrderComponent" href="#createHigherOrderComponent">#</a> **createHigherOrderComponent**

Given a function mapping a component to an enhanced component and modifier
name, returns the enhanced component augmented with a generated displayName.

_Parameters_

-   _mapComponentToEnhancedComponent_ `Function`: Function mapping component to enhanced component.
-   _modifierName_ `string`: Seed name from which to generated display name.

_Returns_

-   `WPComponent`: Component class with generated display name assigned.

<a name="ifCondition" href="#ifCondition">#</a> **ifCondition**

Higher-order component creator, creating a new component which renders if
the given condition is satisfied or with the given optional prop name.

_Parameters_

-   _predicate_ `Function`: Function to test condition.

_Returns_

-   `Function`: Higher-order component.

<a name="pure" href="#pure">#</a> **pure**

Given a component returns the enhanced component augmented with a component
only rerendering when its props/state change

_Parameters_

-   _mapComponentToEnhancedComponent_ `Function`: Function mapping component to enhanced component.
-   _modifierName_ `string`: Seed name from which to generated display name.

_Returns_

-   `WPComponent`: Component class with generated display name assigned.

<a name="useInstanceId" href="#useInstanceId">#</a> **useInstanceId**

Provides a unique instance ID.

_Parameters_

-   _object_ `Object`: Object reference to create an id for.
-   _prefix_ `string`: Prefix for the unique id.

<a name="useKeyboardShortcut" href="#useKeyboardShortcut">#</a> **useKeyboardShortcut**

Attach a keyboard shortcut handler.

_Parameters_

-   _shortcuts_ `(Array<string>|string)`: Keyboard Shortcuts.
-   _callback_ `Function`: Shortcut callback.
-   _options_ `WPKeyboardShortcutConfig`: Shortcut options.

<a name="useMediaQuery" href="#useMediaQuery">#</a> **useMediaQuery**

Runs a media query and returns its value when it changes.

_Parameters_

-   _query_ `[string]`: Media Query.

_Returns_

-   `boolean`: return value of the media query.

<a name="useReducedMotion" href="#useReducedMotion">#</a> **useReducedMotion**

Hook returning whether the user has a preference for reduced motion.

_Returns_

-   `boolean`: Reduced motion preference value.

<a name="useResizeObserver" href="#useResizeObserver">#</a> **useResizeObserver**

Hook which allows to listen the resize event of any target element when it changes sizes.
_Note: `useResizeObserver` will report `null` until after first render_

_Usage_

```js
const App = () => {
	const [ resizeListener, sizes ] = useResizeObserver();

	return (
		<div>
			{ resizeListener }
			Your content here
		</div>
	);
};
```

_Returns_

-   `Array`: An array of {Element} `resizeListener` and {?Object} `sizes` with properties `width` and `height`

<a name="useViewportMatch" href="#useViewportMatch">#</a> **useViewportMatch**

Returns true if the viewport matches the given query, or false otherwise.

_Usage_

```js
useViewportMatch( 'huge', '<' );
useViewportMatch( 'medium' );
```

_Parameters_

-   _breakpoint_ `WPBreakpoint`: Breakpoint size name.
-   _operator_ `[WPViewportOperator]`: Viewport operator.

_Returns_

-   `boolean`: Whether viewport matches query.

<a name="withGlobalEvents" href="#withGlobalEvents">#</a> **withGlobalEvents**

Higher-order component creator which, given an object of DOM event types and
values corresponding to a callback function name on the component, will
create or update a window event handler to invoke the callback when an event
occurs. On behalf of the consuming developer, the higher-order component
manages unbinding when the component unmounts, and binding at most a single
event handler for the entire application.

_Parameters_

-   _eventTypesToHandlers_ `Object<string,string>`: Object with keys of DOM event type, the value a name of the function on the original component's instance which handles the event.

_Returns_

-   `Function`: Higher-order component.

<a name="withInstanceId" href="#withInstanceId">#</a> **withInstanceId**

A Higher Order Component used to be provide a unique instance ID by
component.

_Parameters_

-   _WrappedComponent_ `WPComponent`: The wrapped component.

_Returns_

-   `WPComponent`: Component with an instanceId prop.

<a name="withSafeTimeout" href="#withSafeTimeout">#</a> **withSafeTimeout**

A higher-order component used to provide and manage delayed function calls
that ought to be bound to a component's lifecycle.

_Parameters_

-   _OriginalComponent_ `WPComponent`: Component requiring setTimeout

_Returns_

-   `WPComponent`: Wrapped component.

<a name="withState" href="#withState">#</a> **withState**

A Higher Order Component used to provide and manage internal component state
via props.

_Parameters_

-   _initialState_ `?Object`: Optional initial state of the component.

_Returns_

-   `WPComponent`: Wrapped component.


<!-- END TOKEN(Autogenerated API docs) -->

<br/><br/><p align="center"><img src="https://s.w.org/style/images/codeispoetry.png?1" alt="Code is Poetry." /></p>
