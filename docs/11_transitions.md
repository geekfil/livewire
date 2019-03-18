# CSS Transitions

One of the benefits of using Livewire is utilizing familiar backend functionality like Blade, while making smooth front-ends. Livewire provides a simple CSS Transition system to help acheive this effect.

Livewire provides a basic "fade" transition out-of-the-box.

**view**
```html
<div>
    [...]

    @if($showConfirmationModal)
        <div wire:transition.fade>
            [...]
        </div>
    @endif
</div>
```

When `$showConfirmationModal` is `true`, it's contents are shown. When `$showConfirmationModal` becomes `false`, the contents will fade out, rather than dissapear instantly.

You can control the length of this fade by adding an additional time modifier. The following directive will cause the element to fade in and out for a duration of one second.

`wire:transition.fade.1s`

## Custom transitions

For custom transitions, Livewire uses VueJs's transition syntax.

Let's say we want to add a "fade in and out" transition to a confirmation modal in our component. To achieve this, we need to first declare the transition in our view using Livewire's `wire:transition` directive.

**view**
```html
<div>
    [...]

    @if($showConfirmationModal)
        <div wire:transition="fade">
            [...]
        </div>
    @endif
</div>
```

Now, we need to provide the appropriate CSS selectors in our app's stylesheet for this transition:

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity .2s;
}

.fade-enter, .fade-leave {
  opacity: 0;
}
```

As you can see, Livewire applies the following four classes to the component at different times before adding or removing the element from the page:

Class | Description
--- | ---
.[transition]-enter | is added at the beginning of the transition-in phase, and removed one frame after
.[transition]-enter-active | is added during the entire transition-in phase
.[transition]-leave-active | is added during the entire transition-out phase
.[transition]-leave-to | is added one frame after the transition-out phase begins