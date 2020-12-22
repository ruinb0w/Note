## API

### 登录

```js
request = {
    nickname: "用户名",
    avatar: "用户头像",
    account: "帐号",
    pwd: "密码",
    code: "用户登录凭证"
}

response = {
    token: '用户token'
}
```

### 政协简介

#### 简介内容

```js
response = {
    content: '富文本'
}
```

#### 历届委员

```js
response = [
    {
        times: '第n界',
        list: [ // 人员列表
            {
                avatar: '头像',
                name: '名字',
                position: '职位'
            },
            ...
        ]
    },
    ...
]
```

#### 机构设置

```js
response = [
    {
        title: '标题',
        content: '富文本'
    }
]
```

### 委员信息

```js
response = [
    {
        type: '分类',
        list: [
            {
                avatar: '头像',
            	name: '名字',
            	phone: '电话号码'
            },
            ...
        ]
    },
    ...
]
```

### 公示专栏

#### 专栏列表

```js
response = [
    {
        announce_id: '公示专栏id',
        title: '标题',
        brief: '内容摘录',
        time: '时间',
        pic: '封面'
    }
    ...
]
```

#### 公示专栏详情

```js
request = {
    announce_id: '公示专栏id'
}

response = {
    title: '标题',
    source: '发布主体',
    time: '发布时间',
    content: '发布内容, 富文本'
}
```

### 新闻公告

#### 新闻列表

```js
response = [
    {
        news_id: "新闻id",
        title: '标题',
        brief: '内容摘录',
        time: '时间',
        pic: '封面',
        like: '点赞次数',
        watch: '查看次数'
    }
]
```

#### 新闻详情

```js
request = {
    news_id: "新闻id",
}

response = {
    news_id: "新闻id",
    title: '标题',
    source: '发布主体',
    time: '发布时间',
    content: '发布内容, 富文本',
    like: '点赞次数',
    watch: '查看次数',
    is_like<bool>: '是否对该文章点赞过'
}
```

#### 点赞新闻

```js
request = {
    news_id: "新闻id"
}
```

### 建言献策

```js
request = {
    content: '主要内容',
    name: "名字",
    phone: "电话",
    phone_code: "验证码"
}
```

### 委员提案

#### 提案列表

```js
response =[
    {
    	type: "提案类型",
    	list: [
    	    {
        	    post_id: '提案id'
    			no: '提案编号',
    			title: "提案标题",
    			poster: "提案人姓名",
    			time: "时间",
        	},
        	...
    	]	
	}
]
```

#### 提案详情

```js
requeset = {
    post_id: "提案id"
}

response = {
    title: "标题",
    times: "届/次",
    type: "提案类型",
    secret_level: "保密级别",
    duration: "提出期间",
    poster: "提出人姓名",
    department: "办理部门",
    content: "内容",
    attachment: [
        "附件url",
        ...
    ]
}
```

### 协商在基层

#### 议题列表

```js
request = {
    token
}

response = [
    {
        status: "议题状态",
        list: [
            {
                discuss_id: "议题id"
                title: "议题标题",
                time: "发布时间",
                department: "处理部门"
            },
            ...
        ]
    },
    ...
]
```

#### 议题详情

```js
request = {
    token,
    discuss_id: "议题id"
}

response = {
    title: "议题标题",
    time: "时间",
    poster: "申报人",
    meeting_level: "会议层级",
    content: "内容",
    target: "预期目标",
    pics: ["图片url"],
    status: "议题状态",
    discuss_id: "议题id",
    pics: ["图片url"]
}
```

#### 议题申报

```js
request = {
    token,
    title: "标题",
    time: "时间",
    poster: "申报人",
    meeting_level: "会议层级",
    content: "内容",
    target: "预期目标",
    pics: ["图片url"]
}
```

#### 获取可发起的会议列表

```js
request = {
	token
}

response = [
    {
        meeting_id,
        title: "会议标题"
    }
]
```

#### 发起会议

```js
request = {
    token,
    meeting_id,
    title: "标题",
    date: "会议日期",
    start_time: "会议开始时间",
    end_time: "会议结束时间",
    address: "会议地点",
    compere: "主持人",
    secretary: "会议秘书",
    content: "会议内容"
}
```

### 个人中心

#### 用户信息

```js
request = {
    token
}

response = {
    name: "真实姓名",
    avatar: "头像",
    position: "职位"
}
```

#### 意见反馈

```js
request = {
    content: "反馈内容",
    phone: "电话号码",
    phone_code: "验证码"
}
```

#### 关于

```js
response = {
	content: "关于小程序的内容"
}
```

### 用户相关信息

#### 我的议题

```js
request = {
    token
}

response = [
    {
        status: "议题状态",
        list: [
            {
                discuss_id: "议题id"
                title: "议题标题",
                time: "发布时间",
                department: "处理部门"
            },
            ...
        ]
    },
    ...
]
```

#### 我的会议

```js
request = {
    token
}

response = [
    {
        meeting_id,
        title: '标题',
        address: "会议第点",
        time: "会议时间",
        poster: "发起人",
        phone: "联系电话",
        way: "参会方式",
        content: "会议内容"
    }
]
```

#### 待我审核

```js
request = {
    token
}

response = [
    {
        status: "议题状态",
        list: [
            {
                discuss_id: "议题id"
                title: "议题标题",
                time: "发布时间",
                department: "处理部门"
            },
            ...
        ]
    },
    ...
]
```

### 其它

#### 获取验证码

```js
request = {
    phone: "电话号码"
}
```

#### 图片上传

```js
request = {
    name: "pic", //文件的key
}

response = {
    url: "图片在服务器的url"
}
```

