# @gurinder/vue-confirm

### Installation & Usage

```php
    <vue-confirm></vue-confirm>
```

```js
import Confirm from '@gurinder/vue-confirm';
Vue.component('vue-confirm', Confirm);

Vue.prototype.$confirm = (message, confirmText, cancelText) => {
    return new Promise((resolve, reject) => {
        window.Event.fire("confirm", {
            message: message,
            confirmText: confirmText,
            cancelText: cancelText,
            resolve: resolve,
            reject: reject
        })
    })
};
// Use in vue instance
this.$confirm("Are you ready to delete")


// Bind confirm to vue instance to use like confirm("Are you ready to delete")
const VueApp = new Vue({
    el: '#app'
})

window.confirm = message => VueApp.$confirm(message);

```