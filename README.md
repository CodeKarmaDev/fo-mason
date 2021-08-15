# fo-mason

fo-mason is a css-grid based masonry layout library built with sass.
No javascript required!

In the future css will have native masonry support. you can read more about that 
[here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Masonry_Layout).

This package however works in browsers right now without additional javascript.

## Why?

To have fun and flex my understanding of css-grid, obviously.

## The Method

I think this picture explains it nicely.

[put image here](#)


We create columns and rows and define the size of the rows as 1/3 of the columns.
We let each brick be span 3-6 rows and you have a fo-masonry layout.


```sass
$brick: 20rem;
$cuts: 3;

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
You have to do some adjustments to handle a `gap` accurately

## Limitations

The size of each brick is adjustable but somewhat ridged.
The brick size must be a multiple of your row size.
And its does not expand with your content.

## Usage

Container element
`.mason` > `.mason-vertical` `.mason-horizontal` `.mason-auto`


```html
<div class="mason mason-vertical mason-auto">
  <div class="brick">...</div>
  <div brick-size="2" class="brick">...</div>
  <div class="brick">...</div>
  <div class="brick">...</div>
  ...
</div>  
```

You can define the `brick-size` manually with a brick-size attribute.
With the default settings `0` is a 1x1 square, 
while `3` is slightly larger then a 1x2 rectangle.
The `brick-size` can also take negative values.
```html
<div class="mason mason-vertical">
  <div brick-size="0">...</div>
  <div brick-size="-2">...</div>
  <div brick-size="3">...</div>
  <div brick-size="1">...</div>
  ...
</div>  
```

## Experimenting

You can begin experimenting by cloning the repo 
and hosting the `test/` folder 
with something like [live-server](https://www.npmjs.com/package/live-server).

This tool was built with the some of the newer sass features available in [DartSass](https://sass-lang.com/dart-sass).
If your using [LibSass](https://sass-lang.com/libsass) then you will need to make some adjustments or install a DarkSass package.


