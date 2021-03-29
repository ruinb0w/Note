### install

1.install axios & vue-axios

```bash
npm install --save axios vue-axios
```

2.register axios on vue 

```js
import {createApp} from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
const app = createApp(...);
app.use(VueAxios, axios);
```

### usage

```js
Vue.axios.get(api).then((response) => {
  console.log(response.data)
})

this.axios.get(api).then((response) => {
  console.log(response.data)
})

this.$http.get(api).then((response) => {
  console.log(response.data)
})
```

