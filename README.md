# fo-mason

fo-mason is a css-grid based masonry layout tool built with sass.
No javascript required!

In the future css will have native masonry support. you can read more about that 
[here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Masonry_Layout).

However this package works in browsers right now without additional javascript.

## Why?

To have fun and flex my understanding of css-grid, obviously.

## The Method

I think this picture explains how it works nicely.

![2021-08-14_21-35](https://user-images.githubusercontent.com/5777735/129467538-3c414c71-8dc9-4640-a94d-274c4a07bb5a.png)

We create columns and rows and define the size of the rows as 1/3 of the columns.
We let each brick span 3 to 6 rows and you have a fo-masonry layout.

This is some simplified sass to give you the gist of what is under the hood.
```sass
$brick: 20rem
$cuts: 3

.mason
    --cuts: #{$cuts}
    --brick-span: 0
    
    display: grid    
    justify-content: center
    grid-auto-flow: row dense

.mason-vertical
    grid-template-columns: repeat(auto-fill, #{$brick})
    grid-auto-rows: $brick / $cuts

.mason-auto > *:nth-child(2n)
    --brick-span: 2
.mason-auto > *:nth-child(3n)
    --brick-span: 1

.mason-vertical > *
    grid-row-end: span calc(var(--brick-span) + var(--cuts))
```


## Limitations

The size of each brick is adjustable but somewhat ridged.
The brick size must be a multiple of the row size.
And bricks don't dynamically expand with their content.

## Usage

After installing just drop in a `.mason` class
and pick either `.mason-horizontal` or `.mason-vertical` 
then add a `.mason-auto` class.

```html
<div class="mason mason-vertical mason-auto">
  <div class="brick">...</div>
  <div class="brick">...</div>
  <div class="brick">...</div>
  ...
</div>  
```

You can define the `brick-size` manually with a brick-size attribute.
The default setting of `0` defines a 1x1 square brick, 
`3` makes the brick slightly larger then a 1x2 rectangle.
The `brick-size` can also take negative values.
```html
<div class="mason mason-horizontal">
  <div brick-size="0">...</div>
  <div brick-size="-2">...</div>
  <div brick-size="3">...</div>
  <div brick-size="1">...</div>
  ...
</div>  
```

## Installation & Configuration


### npm

```bash
npm install fo-mason
```

After installing it you can adjust the configuration like so:
```scss
@use 'path/to/node_modules/fo-mason' with (
    $gap: 1em,
    $brick: 16em,
    $cuts: 2,
    $auto: (
        '3n-1': 1,
        '4n': 2,
        '5n+1': 3
    )
);
```

## Experimenting

You can experiment by cloning the repo 
and hosting the `demo/` folder 
with something like [live-server](https://www.npmjs.com/package/live-server).

Use `npm run demo` to apply your changes to the styling in the demo.

This tool was built with some of the newer sass features available in [DartSass](https://sass-lang.com/dart-sass).
If your using [LibSass](https://sass-lang.com/libsass) then you will need to make some adjustments or install a DartSass package.
Unfortunately as of writing this, the live sass compiler available in vscode uses LibSass. 
Jekyll and Rails also currently uses LibSass.






