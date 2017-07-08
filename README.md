# vue-checkbox-toggle

A simple VueJS checkbox replacment thing.

## Installation

First, install it with NPM

```bash
npm install vue-checkbox-toggle
```

Then, import it where needed

```javascript
import vueCheckboxToggle from 'vue-checkbox-toggle';

...
components: {
    vueCheckboxToggle,
}
...
```

Finally, use it like

```vue
<vue-checkbox-toggle
    v-model="val"
    show-labels
    label-checked="on"
    label-unchecked="off"
></vue-checkbox-toggle>
```

## Props

| Prop | Description |
|------|-------------|
|show-labels|Wether or not to show the label|
|label-checked|The label to show when the checkbox is checked|
|label-uncheck|The label to show when the checkbox is unchecked|
|disabled|Disables the control|


