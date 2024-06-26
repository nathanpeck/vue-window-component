# vue-window-component

This is an example of a basic drag and drop window component implemented in Vue.

![](working.webp)

__Usage:__

```html
<Window id="test-window" :top="100" :left="100" :width="400" :height="400" @close="closeWindow()">
  <template #header>
    Test Window
  </template>
  <template #content>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore
    magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
    consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
    pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est
    laborum.
  </template>
</Window>
```

__Links:__

- [App.vue](./src/App.vue) for usage
- [Window.vue](./src/components/Window.vue) for the draggable component itself

__Features:__

- Basic styling.
- Normalization of drops. The window will not allow itself to be dropped partially off the screen.
- Close button that emits an `@close` event.

__Running demo:__

```
bun run dev
```

Open `localhost:5137` in your browser to view the application.
