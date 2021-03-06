# SolidJS Swipe Card

A SolidJS swipeable card component (tinder-like) heavily inspired by [`react-tinder-card`](https://github.com/3DJakob/react-tinder-card).

Bootstrapped using [`tsdx`](https://github.com/jaredpalmer/tsdx).

## Installing

To install, run

```bash
npm install solidjs-swipe-card
# or
yarn add solidjs-swipe-card
```

## Quick Start

```jsx
import { SwipeCard } from 'solidjs-swipe-card';

const App = () => {
    return (
        <div>
            <SwipeCard class="...">
                <div>I'm a Swipe Card!</div>
            </SwipeCard>
        </div>
    );
};
```

## Props

Both [`createSwipeCard`](#createswipecard) and [`SwipeCard`](#swipecard) use the same prop structure, defined in [`SwipeCardProps`](#swipecardprops).

## createSwipeCard

```js
import { createSwipeCard } from 'solidjs-swipe-card';
const { element, ref, apiRef } = createSwipeCard(props);
```

This primitive returns 3 objects:

### `element`

The rendered solid-js component, ready for use.

### `ref`

The ref that attaches directly to the component.

### `apiRef`

The reference to access the methods of the card. See [`SwipeCardRef`](#swipecardref) for the available methods.

## SwipeCard

Under the hood, SwipeCard uses `createSwipeCard`, passing its props and returning the element.

```tsx
import { SwipeCard } from 'solidjs-swipe-card';
let ref;
let apiRef: SwipeCardRef;
//...
<SwipeCard class="..." ref={ref} apiRef={apiRef}>
    <div>I'm a Swipe Card!</div>
</SwipeCard>;
//...
```

## Types

### SwipeCardProps

The type that defines what props [`SwipeCard`](#swipecard) and [`createSwipeCard`](#createswipecard) use.

### `class`

-   optional
-   type: `string`

Additional CSS class(es) to assign to the component.

### `threshold`

-   optional
-   type:`number`
-   default: `300`

The threshold for considering wether or not a card is swiped. It is based on the speed of which the component moves (px/s). A lower number will make it easier to register a swipe, a higher one will make it harder.

### `rotationMultiplier`

-   optional
-   type: `number`
-   default: 7.5

The coefficient of the rotation. A lower number will make it rotate less, a higher one more.

### `maxRotation`

-   optional
-   type: `number`
-   default: 90

The maximum rotation degrees (ranging from `-maxRotation/2` to `+maxRotation/2`) to add when releasing a card.

### `bouncePower`

-   optional
-   type: `number`
-   default: 0.1

The bounce power of which the card will sway back before returning to its original position when [`bringBack`](#bringback) is called.

Keep it between -0.5 and 0.5 to avoid the card flinging on the other side of the screen.

### `snapBackDuration`

-   optional
-   type: `number`
-   default: 300

The duration of the animation (in ms) triggered by [`snapBack`](#snapback).

### `onSwipe`

-   optional
-   type: `(direction: SwipeDirection) => void`
-   default: `() => {}`

The callback to invoke after the card has registered a swipe (before it has finished animating). It will also provide a enum describing the direction of the swipe (see [`SwipeDirection`](#swipedirection)).

### `onSnapBack`

-   optional
-   type: `() => void`
-   default: `() => {}`

The callback to invoke after [`snapBack`](#snapback) has been invoked. It will execute after the card has returned to its original position.

### `apiRef`

-   optional
-   type: [`SwipeCardRef`](#swipecardref)

The reference to access the methods of the card. See [`SwipeCardRef`](#swipecardref) for the available methods.

> NOTE: Currently, to pass it in typescript, you'd need to declare the apiRef as follows: `const swipeCardRef: SwipeCardRef = {};`

### `ref`

-   optional
-   type: `any`

The ref variable that will be forwarded directly to the card component.

### SwipeDirection

The enum that defines a direction defined as follows:

```ts
enum SwipeDirection {
    RIGHT = 'right',
    LEFT = 'left',
    UP = 'up',
    DOWN = 'down'
}
```

### SwipeCardRef

The type that defines the methods available to interact with the element.

#### `snapBack()`

-   Returns `Promise<void>`

It will reset to the original position the card if it has been swiped. Since it is async, it can be awaited if needed.

## Contributing

TODO

## Additional Notes

This is my first library that I'm writing, I'm open to constructive criticism about the repo structure, code quality and design choices.
