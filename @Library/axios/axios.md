## 基本概念

### 请求拦截器

对要发送的数据进行预处理

## axios配置

### 设置超时 timeout

```js
axios.defaults.timeout = 3000;
```

### 设置基础路径 baseURL

```js
axios.defaults.baseURL = 'http://localhost:3000/app' 
```

### 设置请求头 headers

```js
axios.default.headers[ 'mytoken' ] = 'asjdfhjkshdfkhsdjkfhjkhejkf' 
```

### 设置验证信息 Authorization

```js
axios.interceptors.request.use( ()=>{
    config.headers.Athorization = window.sessionStorage.getItem('token');
    return config //在最后必须return config
})
```

## VUE-axios用new FormData()上传文件

因为axios请求拦截器的存在，直接用axios的POST请求是会被拦截掉，数据会处理掉一些。而我们用new FormData()传输文件是不需要做任何处理的。所以就只能饶过axios的拦截。

在全局main.js里用axios.create创建实例

```js
//main.js 
import axios from 'axios'import VueAxios from 'vue-axios' 
var ajax = axios.create({  
    baseURL: 'http://localhost:8082',  
    timeout: 2000,  
    headers: {'Content-Type': 'multipart/form-data'}
}); 
Vue.prototype.ajax = ajax;
```


input文件上传这里先用@change事件获取文件

```html
<input type="file"  accept=".xls,.xlsx"  @change="inputFileChange"> 
```



然后按钮点击事件拿到e.target.files[0]

```js
export default{  
    data () {    
        return {              
            files : ''    
        }  
    },  
    methods : {     
        inputFileChange (e){        
            // input的@change事件拿到数据              
            this.files = e.target.files[0]    
        },
        clicks () {         
    // 上传按钮点击事件      
    if(this.files){        
        // 把文件放入FormData        
        let fd  = new FormData();        
        fd.append("file", this.files);         
        this.ajax.post('upfile.php',fd).then((res) => {          
            console.log(res);                     
        })        
    }    
        }      
    }
}
```



