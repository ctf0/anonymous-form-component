# Requirement

[Axios](https://github.com/mzabriskie/axios)

[Notification Component](https://github.com/ctf0/Notification-Component)

# Intro
- when using with something like laravel, components shouldn't be an add-on complexity layer, instead it should be kept as dump as possible.

- its easier to maintain the app because you can add any extra inputs you want & add the validation logic to the backend without ever touching the components files.

# Usage
**1-** first register the components

- we use ***Bulma*** for styling, but you can change it by editing the components files.

```js
window.axios = require('axios')
window.Vue = require('vue')

// Axios + Laravel
window.axios.defaults.headers.common = {
    'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').getAttribute('content'),
    'X-Requested-With': 'XMLHttpRequest'
};

// Shared Storage
window.StorageHub = new Vue({
    data: {
        formData: {}
    }
})

// Components
Vue.component('MyForm', require('./path/to/Form.vue'))
Vue.component('FormInput', require('./path/to/Input.vue'))
```

**2-** make sure your backend return errors payload as an `array`.

## Example
- MyForm
    ```html
    <my-form inline-template>

        <form action="url"
              method="post"
              class="column"
              @submit.prevent="FormSubmit($event)">

            <!-- form inputs -->
            ...

            <!-- submit -->
            <div class="field">
                <div class="control">
                    <button type="submit"
                            class="button is-info"
                            :disabled="isSubmitting"
                            :class="{'is-loading': isSubmitting}">
                        Submit
                    </button>
                </div>
            </div>
        </form>

    </my-form>
    ```

- FormInput
    ```html
    // for pre-defeined values
    <form-input inline-template>
        <input type="hidden" name="token" value="abc">
    </form-input>

    // for normal inputs
    // :get-errors="errors.inputName"
    <form-input inline-template :get-errors="errors.email">
        <div class="field">
            <label for="email" class="label">E-Mail Address</label>
            <div class="control">
                <input type="email"
                       name="email"
                       class="input"
                       v-model="input"
                       @input="getName($event)"
                       :class="classObject">
            </div>
        </div>
    </form-input>

    // for radio/checkbox
    <form-input inline-template :get-errors="errors.email">
        <div class="field">
            <div class="control">
                <label class="checkbox">
                    <input type="checkbox"
                           name="remember"
                           v-model="input"
                           @click="getName($event)">Remember me
                </label>
            </div>
        </div>
    </form-input>
    ```

- FormErrors
    ```html
    <form-input>
        // ...
        <form-errors :errors="showErrors"></form-errors>
    </form-input>
    ```

## Notes

- This is a combination between showing the form data under **Vue DevTools** while using `FormData()` to send the data to the backend,
however if you dont care about displaying the data under the **DevTools**, you can use [This](https://github.com/ctf0/anonymous-form-component/tree/FormData) instead.

# ToDo
* [ ] Turn into Package.
