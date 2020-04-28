# **可提供一对多转推服务的bot后端**

目前仍然处于测试状态

已经可用，对大部分异常进行了处理(宕机也是宕一半.jpg)

*为了保证推送的正常运行使用了多线程

依赖的模块 nonebot,tweepy

pip安装nonebot,tweepy

将config_example.py改名为config.py并填写内部的配置信息

然后就可以用start.py启动项目了

仅支持 Python 3.7+ 及 CQHTTP 插件 v4.8+。



## 推特监测支持的命令：

注:命令前注意添加前缀，以及注意命令权限要求

注:命令对空格要求严格，参数间必须只空一个空格

### delall

别名：这里单推bot

权限：超级管理员,@bot

功能：移除当前私聊/群的所有监测

### getpushlist

别名：DD列表

权限：无限制

功能：获取当前私聊/群的监测列表

![image-20200428114040218](https://raw.githubusercontent.com/chenxuan353/tweetToQQbot/master/readme/image-20200428114040218.png)

### getuserinfo 推特用户ID/用户名(非昵称)

别名：查询推特用户

权限：超级管理员,@bot

功能：获取当前私聊/群的监测列表

例：getuserinfo shiranuiflare

![image-20200428113938381](https://raw.githubusercontent.com/chenxuan353/tweetToQQbot/master/readme/image-20200428113938381.png)

### addone 推特用户ID/用户名(非昵称) 昵称 描述

别名：给俺D一个

权限：超级管理员,@bot

功能：添加一个用户到本群监测

例如：给俺D一个 shirakamifubuki 吹雪 我永远喜欢小狐狸

不需要设置昵称：给俺D一个 shirakamifubuki  我永远喜欢小狐狸

注意：不需要设置昵称的情况下空格不能省略

![image-20200428113806819](https://raw.githubusercontent.com/chenxuan353/tweetToQQbot/master/readme/image-20200428113806819.png)

### delone 推特用户ID/用户名(非昵称)

别名：我不想D了

权限：超级管理员,@bot

功能：移除一个本群监测的用户



### getGroupSetting

别名：全局设置列表

权限：无限制

功能：显示当前私聊/群的全局推送设置



### getSetting 推特用户ID

别名：对象设置列表

权限：无限制

功能：显示当前私聊/群的某个监测对象的推送设置



### setGroupAttr 属性 值

别名：全局设置

权限：超级管理员,@bot

功能：移除一个本群监测的用户

例：setGroupAttr 转推 关

#### 支持的属性列表(大小写不敏感)：

注：属性名称，别名1，...，别名n

##### 	携带图片发送

​	upimg，图片，img

#####     消息模版(参数为模版字符串)

​    retweet_template,转推模版

​    quoted_template,转推并评论模版

​    reply_to_status_template,回复模版

​    reply_to_user_template,被提及模版

​    none_template,发推模版

#####     推特转发各类型开关

###### 	属性

​    retweet,转推

​    quoted,转推并评论

​    reply_to_status,回复

​    reply_to_user,被提及

​    none,发推

###### 	支持的值

​	true,开,打开,开启,1

​	false,关,关闭,0

#####     推特个人信息变动推送开关

###### 	属性

​    change_id,ID改变

​    change_name,名称改变

​    change_description,描述改变

​    change_headimgchange,头像改变

###### 	支持的值

​	true,开,打开,开启,1

​	false,关,关闭,0

#### 模版字符串说明

##### 默认模版

###### 	发推

```
推特ID：$tweet_id_min，【$tweet_nick】发布了：\n$tweet_text
```

###### 	转推

```
推特ID：$tweet_id_min，【$tweet_nick】转了【$related_user_name】的推特：\n$tweet_text\n====================\n$related_tweet_text
```

###### 	转发并评论

```
推特ID：$tweet_id_min，【$tweet_nick】转发并评论了【$related_user_name】的推特：\n$tweet_text\n====================\n$related_tweet_text
```

###### 	回复与被提及

```
推特ID：$tweet_id_min，【$tweet_nick】回复了【$related_user_name】：\n$tweet_text
```

##### 模版支持的变量

​	注：使用\n替代换行符，理论上直接换行也可以但是十分不推荐(

​      $tweet_id 推特ID

​      $tweet_id_min 压缩推特id

​      $tweet_nick 操作人昵称

​      $tweet_user_id 操作人ID

​      $tweet_text 发送推特的完整内容

​      $related_user_id 关联用户ID

​      $related_user_name 关联用户昵称-昵称-昵称查询不到时为ID(被评论/被转发/被提及)

​      $related_tweet_id 关联推特ID(被评论/被转发)

​      $related_tweet_id_min 关联推特ID的压缩(被评论/被转发)

​      $related_tweet_text 关联推特内容(被转发或被转发并评论时存在)



### setAttr 监测用户UID 属性 值

别名：对象设置

权限：超级管理员,@bot

功能：移除一个本群监测的用户

例：setGroupAttr 997786053124616192 转推 关

注：UID可以通过命令getpushlist查看



