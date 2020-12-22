### 修复

1. `/service/getHouseDetail`

   ```json
   // request
   {
       url: 'https://api.lcwmkj.cn/service/service/getHouseDetail?token=b0pPVkw1RHRQUjNkaUc4SXBjUUg4MjFWRGt2WWxjemhzcXRva2Vu',
       data: {
       	id: 56
   	}
   }
   
   // response
   {
       ...
       start_time: "1970-01-01"
   }
   ```

### 修改

1. `/forum/posting_list` 
   * 加上`is_finished`, 默认false, 通过完成心愿改为true

### 新增

1. 完成心愿

   ```json
   // request
   {
       post_id: 帖子id
   }
   ```

2. 通过论坛建立私信

   ```json
   // request
   {
       reply_id: 对评论发起私信,
       post_id: 对帖子主人发起私信
   }
   // response
   {
       id: 私信表id
   }
   ```

3. 发私信

   ```json
   // request
   {
       content: 私信内容,
       id: 私信表id
   }
   ```

4. 私信列表

   ```json
   // response
   {
       [
       	avatar: 对方的头像,
       	nickname: 对方的名字,
      		time: 对方最后一句话的时间戳,
       	content: 对方最后一句话,
       	is_read: 是否看过,
       	id: 私信表id
       ],
       unread_num: 总未阅读数
   }
   ```

5. 私信详情

   ```json
   // request
   {
       id: 私信表id
   }
   // response
   {
       mine: [ // 自己
           {
               content: 内容,
               time: 时间戳
           }
       ],
       opposite: [ // 对方
           {
               content: 内容,
               time: 时间戳
           }
       ]
   }
   ```

   

