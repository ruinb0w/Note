### 招聘求职

1. 行业类型, 类型为空

   ```
   https://fqapi.lcwmkj.cn/work/company_type?token=b3FOWTA1Z2wtcUlrVHVoZ3Q3ZFhxMzdXeWxOQWZxemhzcXRva2VuODg4ODg=
   
   code: 10000
   data: [] 
   msg: "ok"
   ```

2. 我的求职详情, 加是否公开手机号

   ```
   https://fqapi.lcwmkj.cn/work/resume_detail?token=b3FOWTA1Z2wtcUlrVHVoZ3Q3ZFhxMzdXeWxOQWZxemhzcXRva2VuODg4ODg=
   
   add_time: "2021-03-23"
   address: "测试"
   birth: "2021-03-23"
   certification: "测试"
   desc: "测试"
   education: "高中及以下"
   exp: "测试"
   gender: "男"
   id: "1"
   name: "测试"
   other: "测试"
   phone: "17308837960"
   pics: "http://fq-sh-oss.lcwmkj.cn/img-public/Upimg/fqxcx/resume_pics/2021-03-23/605962b2d3195.jpeg;http://fq-sh-oss.lcwmkj.cn/img-public/Upimg/fqxcx/resume_pics/2021-03-23/605962b34c915.jpeg;"
   politic: "群众"
   race: "汉族"
   school: "测试"
   specialty: "测试"
   status: "1"
   uid: "3"
   ```

3. 修改求职, 无法修改

   ```
   https://fqapi.lcwmkj.cn/work/add_job_search?token=b3FOWTA1Z2wtcUlrVHVoZ3Q3ZFhxMzdXeWxOQWZxemhzcXRva2VuODg4ODg=
   
   data: {"id":"1","type":"全职","position":"测试","memo":"测试公开手机号","salary":"500-1500","address":"全临沧","is_phone":"否","is_resume":"否"}
   
   code: 10009
   data: null
   msg: "请勿重复提交！"
   ```

### 租房服务

1. 房屋列表

   ```
   https://fqapi.lcwmkj.cn/house/house?token=b3FOWTA1Z2wtcUlrVHVoZ3Q3ZFhxMzdXeWxOQWZxemhzcXRva2VuODg4ODg=
   
   1146:Table 'fengqing_db.pigcms_house_village_store_house' doesn't exist [ SQL语句 ] : SHOW COLUMNS FROM `pigcms_house_village_store_house`
   错误位置
   FILE: /www/wwwroot/fengqing.lcwmkj.cn/ThinkPHP/Library/Think/Db/Driver.class.php 　LINE: 350
   ```

### 报事

1. /gongdan/AddUserGongdan

   ```
   https://fqapi.lcwmkj.cn/gongdan/AddUserGongdan?token=b3FOWTA1Z2wtcUlrVHVoZ3Q3ZFhxMzdXeWxOQWZxemhzcXRva2VuODg4ODg=
   
   content: 测试2
   title: 测试2
   type: 1
   q_id: 92
   img: http://fq-sh-oss.lcwmkj.cn/img-public/Upimg/fqxcx/Gongdan/2021-03-23/605952ea0f857.jpeg;
   lng: 100.08233
   lat: 23.89516
   address: 云南省临沧市临翔区忙令南路
   
   code: 10009
   data: null
   msg: "请选择上报方式"
   ```
