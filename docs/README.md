---
layout: HomeLayout
home: true
heroImage: /logo.svg
heroText: Vue Formulate
tagline: The easiest way to build forms with Vue
actionText: Get Started →
actionLink: /guide/
features:
- title: 😎 Developer happiness
  details: Forms are everywhere, yet surprisingly tedious to author — well, not anymore. Vue Formulate provides a powerful and flexible API to developers that makes complex form creation a breeze.
- title: ☝️ A single input element
  details: With Vue Formulate you don't need to remember the names of a dozen components — all form elements are created with a single component. Easy!
- title: 💪 Grouped fields
  details: Vue Formulate ships with repeatable field groups out of the box. Create complex UIs such as multi-person booking forms with ease.
- title: 🎯 Built-in validation
  details: Ridiculously easy validation out-of-the-box to handle 95% of use-cases. Help text, validation rules, and validation messages are simple props. Need more? You can add custom validations too.
- title: 🔌 Plugin system
  details: Extend Vue Formulate's functionality or reuse custom inputs, validation rules, and messages across projects by tapping into the plugin system. Make your plugin open source to share with others!
- title: ✨ Form Generation
  details: Generate an entire form from JSON. Vue Formulate includes a schema to allow you to render complex forms from JSON with groups, wrappers, and custom components.
- title: 🎨 Styling Control
  details: With provided class props you can add your own set of style classes globally or on a case-by-case basis. Tailwind? No problem. Bootstrap? You're covered. Roll your own? Right on, it’s supported.
- title: 🔍 Scoped Slots
  details: Need even more control over your form’s markup? Vue Formulate ships with full scoped slots support so that you can globally or selectively provide your own markup.
- title: 🌐 Internationalization
  details: Thanks to the wonderfully collaborative Vue community, Vue Formulate ships with support for over a dozen languages which are selectively importable to keep bundle size light.
---
# Live Code Examples

### Form validation
Vue Formulate includes [20 rules](/guide/validation/) and support for defining your own.

<ClientOnly>
  ```html live
  <FormulateInput
    type="email"
    label="What is your school email address?"
    validation="bail|required|email|ends_with:.edu"
    validation-name="School email"
    placeholder="user@university.edu"
  />
  ```
</ClientOnly>


### Single-element inputs
Try changing `type="radio"` to `checkbox` or `select` in this demo.

<ClientOnly>
```html live
<FormulateInput
  type="radio"
  label="What do you think of Vue Formulate?"
  :options="{
    good: 'It’s good',
    great: 'It’s great',
    install: 'I’m installing it now.'
  }"
/>
```
</ClientOnly>

### Well-considered file inputs
[File inputs](/guide/inputs/types/file/) done well, right out of the box.

<ClientOnly>
```html live
<FormulateInput
  type="image"
  label="Gallery Images"
  validation="mime:image/jpeg,image/jpg,image/png"
  help="Don’t worry — our demo doesn't upload your image"
  multiple
/>
```
</ClientOnly>

### Model an entire form in one object
Effortlessly ensure all fields have validated and even `v-model` field values
to a single object.

<ClientOnly>
```vue live
<template>
  <!-- some code condensed for display reasons -->
  <FormulateForm
    v-model="values"
    @submit="handleLogin"
  >
    <h2>Login</h2>
    <FormulateInput type="text" name="email" label="Email address" validation="required|email" />
    <FormulateInput type="text" name="password" label="Password" validation="required" />
    <FormulateInput name="terms" type="checkbox" label="I accept, just don't make me read the terms." validation="accepted" />
    <FormulateInput type="submit" label="Login" />
    <pre>{{ values }}</pre>
  </FormulateForm>
</template>

<script>
export default { data () { return { values: {}, handleLogin: () => alert('Logged in') } } }
</script>
```
</ClientOnly>


### Quickly implement complex repeatable fields
Add [grouped](/guide/inputs/types/group/) and [repeatable](/guide/inputs/types/group/#repeatable-groups)
fields without the complexity.

<ClientOnly>
```vue live
<template>
  <!-- some code condensed for display reasons -->
  <FormulateForm v-model="values" @submit="submitHandler">
    <h2>Frosty's Frozen Treats</h2>
    <FormulateInput
      type="group"
      name="flavors"
      label="Create your custom order"
      help="Choose your hand-packed pints whipped up by our expert servers"
      add-label="+ Add Flavor"
      validation="required"
      :repeatable="true"
    >
      <div class="order">
        <FormulateInput name="flavor" type="select" label="Flavor" validation="required" :options="{ vanilla: 'Vanilla', chocolate: 'Chocolate', strawberry: 'Strawberry', pineapple: 'Pineapple'}" />
        <FormulateInput name="quantity" label="Quantity" type="number" min="1" validation="required|min:1" />
      </div>
    </FormulateInput>

    <FormulateInput name="deliveryMethod" type="radio" label="Delivery Method" validation="required" :options="{ local: 'Local Pick-up', delivery: 'Delivery (5-mile radius)' }" />
    <FormulateInput name="orderNotes" type="textarea" label="Order Notes" help="Allergies? Delivery instructions? Don't need the spoons? Let us know!" />
    <FormulateInput type="submit" value="Place Order" />
    <pre>{{ values }}</pre>
  </FormulateForm>
</template>

<script>
export default { data () { return { values: {} } }, methods: {submitHandler () { alert(`Thank you for your order!`) } } }
</script>
```
</ClientOnly>
