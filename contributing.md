# Contributing

When you look into /src, it seems there are shit loads of codes, but as mentioned in https://github.com/YIZHUANG/react-multi-carousel/blob/master/README.md that 80% of the code in this libirary are about making the `Infinite mode` work. Trust me, i have already tried my best to refactor them, but there are too many edge cases for the `Infinite mode`, and requires extra amount of codes to handle them, i have already tried my best to comment the codes. It's not perfect code but i can say its so much better than ```react-slick```

## Infinite mode

If you are interested in contributing, and you are making a feature/fixing a bug that's related or not related to the `Infinite mode`, its important for you to know which files/codes are for infinite mode and which files/codes are not for the `Infinite mode`, so that you don't get confused.

Here are a list of files/functions that are for the infinite mode only, if you are making a feature/fixing a bug that's not related to the `Infinite mode` you can safely ignore them.

- throttle
- getOriginalCounterPart
- getCloneCounterPart
- getClones
- whenEnteredClones
- correctClonesPosition() in componentDidUpdate()
- setClones()

## Technical guide.

The most difficult part of building this lib is for the infinite mode. For non-infinite mode, its very easy, we simply calculate the length of the children as well as calculating the total width of the container, and then the following:

```
const width = containerWidth / this.props.children.length;
return children.map(child => <li style={{ width: width }}>{child}</li> )
```

And this is what's behind of hood pretty much.

For for the infinite mode, we need to clone the children on the client-side, the algorithm that is used in this lib can be found at `utils/clones` with the name `getClones()`.

We also need to care about the timing of canceling/enabling the animation, there are two functions for this, can be found at `utils/clones` with the name `whenEnteredClones()` and `correctClonesPosition()` in `Carousel.tsx` in the `componentDidUpdate()` method.

For server-side rendering, we use `flex-basis` to set the width of the item, and on the client-side we switch to `width`

## Locale development.

- cd app
- npm install
- npm run dev