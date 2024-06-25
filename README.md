# Popover <!-- omit in toc -->

## Element

<https://caniuse.com/?search=popover>

1. Add `popover` to any element to turn it into a popover.

    ```html
    <div id="popover-message" popover>Message for the popover</div>
    ```

1. Add a `button` element with `[popovertarget="popover-message"]` referencing the popover element.

    ```html
    <button popovertarget="popover-message">toggle</button>
    ```

1. Click the `button` to toggle the popover display.

- Popovers always display on the top layer, the highest z-index value.

## States

### `popover=auto`

- Default mode.
- Only 1 popover can be in `auto` state.
- Un-displayed popovers have `display: none`.
- Displayed popovers have `display: block`.

To dismiss:
    - Click button same button.
    - Click button with `popovertargetaction="hide"`.
    - Click anywhere on page.
    - Press <kbd>esc</kbd>.

### `popover=manual`

To dismiss:
    - Click button same button.
    - Click button with `popovertargetaction="hide"`.

### Popover Target action

By default, a button toggles the popover between `show` and `hide` states.

- `popovertargetaction="show"` will show the popover but won't hide on click
- `popovertargetaction="hide"` will hide the popover but won't show on click

### Javascript

When using JavaScript, the trigger element is NOT restricted to `<button>`; it can be anything.

```js
function show() {
    document.getElementById('popover-message').showPopover()
}
function hide() {
    document.getElementById('popover-message').hidePopover()
}
```

To automatically hide the popover after 2 seconds.

```js
function show() {
    document.getElementById('popover-message').showPopover()
    setTimeout(() => hide(), 2000);
}
```

## Styling

```css
[popover] {
    width: 100%;
    max-width: 20rem;
    padding: 1rem;
    border-radius: .5rem;
    background: hsl(0, 0%, 25%);
    color: hsl(220, 14%, 96%);
}
```

Popovers can NOT be positioned relative. They must be manually positioned.

### Animation

Animating popover displays is a little complex.

```css
[popover] {
    opacity: 0;
    transition: all .5s allow-discrete;
}

[popover]:popover-open {
    opacity: 1;
}


/* Needs to be included after the previous [popover]:popover-open
   rule to take effect, as the specificity is the same
   @see https://developer.mozilla.org/en-US/docs/Web/CSS/transition-behavior
*/
@starting-style {
    [popover]:popover-open {
        opacity: 0;
    }
}
```

### Backdrop

Unlike the `dialog` element, `popup` does NOT disable background pointer functions. This makes styling the backdrop obsolete.

```css
[popover]::backdrop {
    backdrop-filter: blur(3px);
}
```
