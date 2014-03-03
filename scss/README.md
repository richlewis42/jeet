# Jeet for SCSS

Jeet is the most advanced, yet intuitive, grid system on the market today.

#### Installation
- Install Ruby [[Windows](http://rubyinstaller.org/), [Mac/Linux](https://github.com/sstephenson/rbenv)]
- `gem install sass`
- `cd ~/Project/css`
- `svn checkout https://github.com/mojotech/jeet/trunk/scss/jeet`
- Put `@import 'jeet/index.scss';` at the top of `~/Project/css/foo.scss`

#### Usage
```
sass -w foo.scss
```

#### Usage Example
```html
<html>
  <head>
    <link rel="stylesheet" href="css/foo.css">
  </head>
  <body>
    <section>
      <aside>Sidebar</aside>
      <article>Content</article>
    </section>
  </body>
</html>
```

```scss
@import 'jeet/index.scss';
@include edit();

section {
 @include center();
}
aside {
 @include col(1/3);
}
article {
 @include col(2/3);
}
```

#### API
- **`column($ratios: 1, $offset: 0, $cycle: 0, $uncycle: 0, $gutter: $jeet-gutter)`** - `column` (also aliased as `col`) is perhaps the strongest feature of any grid system on the market. You specify an initial ratio, either as fractions or decimals, then pass the parent container's context ratio to maintain consistent gutters as you nest. Offsetting is made trivial as well. Just specify a ratio to make your offset have a margin-left. Make it negative to give it a margin-right instead. E.g. `column(1/4, $offset: 1/4)` would create a column the quarter of the size of it's container and push it to the right a quarter. `cycle` and `uncycle` are pretty awesome in their own right as well. Want to make a gallery but don't want to specify a row every 4 pictures? `column(1/4, $cycle: 4)` - done. Want to change it up when you get down to mobile? Maybe just show 2 images per row? `uncycle` your 4-item cycle then... `column(1/2, $uncycle: 4, $cycle: 2)` - done. Need to adjust column gutters for a specific container? `col(1/4, $gutter: .5)`
- **`span($ratio: 1, $offset: 0)`** - Need a grid without the gutters? For instance, for a horizontal navigation where you want buttons touching. Do so like: `span(1/5)`. No need to pass more than one ratio since we don't need to worry about the math involved with gutters and all that.
- **`shift($ratios: 0, $col_or_span: column, $gutter: $jeet-gutter)`** - Source ordering works in Jeet by assigning `position: relative` and then a `left` offset equal to the ratio passed. You can specify if this is a column or span shift to include gutters or not. This works similar to `offset` in that it can accept negative values to shift the other direction. Again, `shift` can accept multiple context ratios to maintain perfect sizing. `shift` also accepts custom gutter sizing, just make sure your gutter sizes match the gutter sizes of your original elements.
- **`unshift()`** - Accepts no values but isn't a block closer either. `unshift()` is a great helper function to quickly disable whatever source ordering you've done to an element.
- **`edit()`** - Edit mode assigns a light gray, semi-transparent, background to every element on the page. It's a little trick picked up over the years that makes visualizing the structure of your site trivial.
- **`center($max_width: 1410px, $pad: 0)`** - This is a shortcut to easily center containers. The pad variable sets padding on the left and right.
- **`stack($pad: 0, $align: false)`** - A helper mixin to "stack" elements on top of each other. Useful for mobile views. Accepts padding and/or text alignment.
- **`unstack()`** - Cancel that `stack()`. This won't revert back to your `column()` calls. For that, manually call your `column()` method again.
- **`align($direction: both)`** - Aligning blocks relative to their container with `position: absolute` and fancy positioning and transform. Vertical alignment is now trivial in IE9+ browsers.
- **`%cf`** - The clearfix placeholder saves space on repetitive use of clearfix. Use clearfix anywhere like so: `@extend %cf;`


#### Global Settings
- Create a `_settings.scss` file in your Jeet directory. `@import 'jeet/_settings.scss';` at the top (right above `@import 'jeet/index.scss';`) of whichever file Sass is watching (e.g. `sass -w css/style.scss`).
- You can adjust the following variables:
  - **`$jeet-gutter: 3`** - The percentage of the page the root-level gutters take up.
  - **`$jeet-parent-first: false`** - When assigning multiple ratio contexts to a `col()`, do you want to reference the outer most container first? Example: Let's assume we have a column set to `col(1/4)` that is nested inside of another column that is `col(1/3)` which is nested inside of another column that is `col(1/2)`. By default, to maintain consistently sized gutters (even when nesting), our inner-most column would look like `col(1/4 1/3 1/2)`. If we adjust this global variable to be `true`, our inner-most column could be written from a top-down perspective like so: `col(1/2 1/3 1/4)`. This is entirely a preference thing. Do you like stepping up or down?
  - **`$jeet-layout-direction: LTR`** - Support for left-to-right, or right-to-left (`RTL`) text/layouts.


---

#### Thanks
- **[Jeff Escalante](https://github.com/jenius)** - For his patience and guidance with this project.
- **[Gabriel Manricks](http://gabrielmanricks.com)** - For constantly helping. The man is unstoppable.
- **[Mitchell Coote](http://monkeez.com)** - For contributing the sweet goodness of consistently sized gutters even in nested contexts (seriously-tricky-business).
- **[Carrot Creative](http://carrot.is)** - For keeping up with Jeet and using it on some of the [biggest companies](http://carrot.is/creative) in the world.
- **[The rest of ya's](https://github.com/mojotech/jeet/graphs/contributors)** - Thanks for your love. It makes developing this project fun and rewarding for everyone.