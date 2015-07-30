# Xbox API文档 v0.1

> 1st 2015.07.21 by yy

* 页面
	* \#1
		* [GET /user/nearby_info](#nearby) 获取附近箱子或商品信息
	* \#2
		* [POST /user/apply_box](#applybox) 申请新箱子
	* \#3
		* [GET /user/show](#userShow) 获取用户信息
		* [POST /box/receive_box](#receiveBox) 接收新箱子
		* [POST /box/bind_box](#blindBox) 绑定新箱子
		* [GET /box/products](#showProducts) 显示箱子内货物
		* [POST /products/confirm_inbox](#confirmInBox) 确认消费盒子中某商品
		* [POST /products/unconfirm_inbox](#unconfirmInBox) 取消确认消费盒子中某商品
	* \#4
		* [POST /box/change_box](#changeBox) 换箱子
		* [GET /box/info](#boxInfo) 获取箱子信息
	* \#5
	* \#6
	* \#7
		* [GET /bills/mine](#mineBill) 获取我的账单
	* \#8
		* [GET /bills/show](#showBill) 查看详细账单
		* [POST /products/like](#like) 喜欢某个商品
		* [POST /products/unlike](#unlike) 取消喜欢某个商品
		* [POST /products/confirm_inbill](#confirmInBill) 确认消费账单中某未确认商品
		* [POST /payment/pay](#pay) 支付
	* \#9
		* [POST /products/like](#like) 喜欢某个商品
		* [POST /products/unlike](#unlike) 取消喜欢某个商品
		* [GET /products/fanfan_show](#fanfanShow) 翻一番获取
	* \#10
	* \#11
		* [POST /payment/pay](#pay) 支付
	* 其他
		* [POST /user/sms_verify](#verify) 验证短信
		* [POST /user/sign_up](#signup) 注册
		* [POST /user/get_token](#getToken) 登陆获取token
* 类型
	* user
		* [POST /user/apply_box](#applybox) 申请新箱子
		* [POST /user/sms_verify](#verify) 验证短信
		* [POST /user/sign_up](#signup) 注册
		* [POST /user/get_token](#getToken) 登陆获取token
		* [GET /user/show](#userShow) 获取用户信息
	* box
		* [POST /box/change_box](#changeBox) 换箱子
		* [POST /box/receive_box](#receiveBox) 接收新箱子
		* [POST /box/bind_box](#blindBox) 绑定新箱子
		* [GET /box/products](#showProducts) 显示箱子内货物
		* [GET /box/info](#boxInfo) 获取箱子信息
	* bills
		* [GET /bills/mine](#mineBill) 获取我的账单
		* [GET /bills/show](#showBill) 查看详细账单
	* products
		* [POST /products/like](#like) 喜欢某个商品
		* [POST /products/unlike](#unlike) 取消喜欢某个商品
		* [POST /products/confirm_inbox](#confirmInBox) 确认消费盒子中某商品
		* [POST /products/unconfirm_inbox](#unconfirmInBox) 取消确认消费盒子中某商品
		* [POST /products/confirm_inbill](#confirmInBill) 确认消费账单中某未确认商品
		* [GET /products/fanfan_show](#fanfanShow) 翻一番获取
	* payment
		* [POST /payment/pay](#pay) 支付
	* 其他
		* [GET /user/nearby_info](#nearby) 获取附近箱子或商品信息
		




<h2 id="nearby">GET /user/nearby_info </h2>
### Summary
 #1页，获取周边信息用于新用户浏览
### Description
一开始用户较少，返回杭州本地的信息即可。无需返回身边。
### Parameters
无
### Responses
	<json>
	{
		"numberOfNearbyBox":Int,
		"numberOfNearbyUser":Int,
		"numberOfNearbyProduct":Int,
		"boxImages":[
			boxImageSmall:String
		],
		"userAvatars":[
			userAvatarSmall:String
		],
		"productImages":[
			productImageSmall:String
		]
	}
	
<h2 id="applybox">POST /user/apply_box </h2>
### Summary
 #2页，申请新箱子
### Description
新用户递交申请
### parameters
 name | required | type | note 
 --- | --- | ---| --- 
 phoneNumber | true | String | 电话号码
 cityCode | true | Int | 城市列表 
 areaCode | true | Int | 区列表 
 speficLocation | true | String | 详细地址 
 sexualBiasCode | true | Int | 性别偏好
### Responses
成功申请与否

<h2 id="verify">POST /user/sms_verify</h2>
### Summary
发送验证短信
### Description
### parameters
 name | required | type | note 
--- | --- | --- | ---
 phoneNumber | true | String | 待验证电话号码  
### Responses
是否发送成功

<h2 id="signup">POST /user/sign_up</h2>
### Summary
 注册
### Description
新用户注册流程：填写手机号，昵称，收到验证码注册
### parameters
 name | required | type | note 
--- | --- | --- | ---
 phoneNumber | true | String | 注册电话号码 
 verificationCode | true | String | 验证码 
 nickName | true | String | 昵称 
### Responses
是否注册成功


<h2 id="getToken">POST /user/get_token</h2>
### Summary
登录/获取token
### Description
### parameters
 name | required | type | note 
--- | --- | --- | ---
 phoneNumber | true | String | 手机号 
 password | true | String | 密码 
### Responses
验证成功，返回token




<h2 id="userShow">GET /user/show</h2>
### Summary
获取登录用户的信息
### Description
登录之后获取登录用户信息，用于首页呈现等
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 用户id 

### Responses
	<json>
	{
		"id": String
		"nickName": String, //昵称
		“phoneNumber”: String, //电话号码
		"money": double, //账户余额
		"boxes": [
			"id": String, 
			"name": String,
			"location": String
		], //绑定的盒子
		"avatar": String //头像地址	
	}
	
<h2 id="changeBox">POST /box/change_box</h2>
### Summary
换箱子
### Description
相服务端申请换箱，服务端判断是否达到条件，返回申请成功与否。
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 箱子的编号  
### Responses
是否成功，不成功的理由？(时间或者有账单未支付)

<h2 id="receiveBox">POST /box/receive_box</h2>
### Summary
接到新箱
### Description
申请换箱服务后，新箱送达，扫描确认收到新箱。老箱回收。

后台给其他用户推送消息。
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 箱子的编号  
### Responses
是否成功。

<h2 id="blindBox">POST /box/bind_box</h2>
### Summary
绑定新的箱子
### Description
新用户扫描箱子进行绑定
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 boxid | true | String | 箱子的编号  
 userid | true | String | 用户编号 
### Responses
绑定是否成功

<h2 id="showProducts">GET /box/products</h2>
### Summary
 #3页，获取盒子的商品
### Description
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 箱子的编号  
### Responses
	<json>
	{
		"products":[
			"id": String, //商品编号
			"name": String, //商品名称
			"price": double, //零售价
			"salePrice": double, //实际卖价
			"image": String //图片url 
			"sold": Bool //是否已售出
		]
	}

<h2 id="boxInfo">GET /box/info</h2>
### Summary
 #4页，获取盒子的信息
### Description
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 箱子的编号  
### Responses
	<json>
	{
		"id":String,
		"name":Int,
		"location":String, //"浙江省杭州市西湖区XXXX"
		"boxType":String, //规格，small,medium,big
		“users”: [
			userId:String,
			userName:String,
			userAvatarSmall:String, //地址，小图
		]
		"applyReplace":Bool //是否已经申请了换箱
	}


<h2 id="mineBill">GET /bills/mine</h2>
### Summary
 #7页，获取我的所有账单
### Description
获取用户历史账单，包括待付账单。
### parameters
 name | required | type | note 
  --- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 用户编号  
### Responses
	<json>
	{
		"id": String, //账单id
		"time": Date, //账单生成时间
		"boxName": String, //账单对应box名称
		“debt”: Double, //账单数额
		“status”: Int, // 2,待确认 1，待付款  0，已付款
	}

<h2 id="showBill">GET /bills/show</h2>
### Summary
获取账单详细信息
### Description
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 账单编号  
### Responses
	<json>
	{
		"time": Date, //账单生成时间
		"boxName": String, //账单对应box名称
		“debt”: String, //账单总额，现阶段就是消费金额
		“expense”: Double, //消费金额，即购买的商品的金额
		"unSelDebt": Double, //box未选择消费商品的总值
		"paid": Bool, //是否已经支付
		“products”: [
			"id": String,
			"name": String,
			"salePrice": double,
			“image”: String,
			“liked”: Bool //是否喜欢了该商品
		]
		"unSelProducts": [
			“id”: String, //商品id
			“name”: String,
			"salePrice": double, //实际卖价
			“image”: String
		] //未选择的商品
	}


<h2 id="like">POST /products/like</h2>
### Summary
喜欢了某个商品
### Description
点击喜欢某个商品，从而影响下一次箱子的配送
### parameters
 name | required | type | note 
  --- | --- | --- | ---
 token | true | String | 令牌 
 productId | true | String | 商品编号  
### Responses
确认是否成功

<h2 id="unlike">POST /products/unlike</h2>
### Summary
取消喜欢某个商品
### Description
取消对某个商品的喜欢
### parameters
 name | required | type | note 
 --- | --- | --- | ---
 token | true | String | 令牌 
 productId | true | String | 商品编号  
### Responses
确认是否成功

<h2 id="confirmInBox">POST /products/confirm_inbox</h2>
### Summary
确认消费
### Description
通过扫描或点击，确认消费了箱子中的商品
### parameters
 name | required | type | note 
   --- | --- | --- | ---
 token | true | String | 令牌 
 boxId | true | String | box编号 
 productId | true | String | 商品编号 
### Responses
是否确认成功

<h2 id="unconfirmInBox">POST /products/unconfirm_inbox</h2>
### Summary
取消确认消费
### Description
取消消费
### parameters
 name | required | type | note 
--- | --- | --- | ---
 token | true | String | 令牌 
 boxId | true | String | box编号 
 productId | true | String | 商品编号 
### Responses
是否取消成功

<h2 id="confirmInBill">POST /products/confirm_inbill</h2>
### Summary
确认未选择消费
### Description
从账单中确认自己消费了却未确认的消费
### parameters
  name | required | type | note 
  --- | --- | --- | ---
 token | true | String | 令牌 
 billId | true | String | 账单编号 
 productId | true | String | 商品编号  
### Responses
确认是否成功


<h2 id="fanfanShow">GET /products/fanfan_show</h2>
### Summary
获取翻一翻中的商品
### Description
每次获取有限个之前未标注过喜欢的商品。
### parameters
 name | required | type | note 
  --- | --- | --- | ---
 token | true | String | 令牌 
 id | true | String | 用户编号 
 num | true | Int | 一次获取多少商品 
### Responses
	<json>
	{
		"products":[
			"id": String, //商品编号
			"name": String, //商品名称
			"price": double, //零售价
			"image": String //图片url 
			"numberOfLike": Int //被喜欢的次数
		]
	}

<h2 id="pay">POST /payment/pay</h2>
### Summary
请求账单支付订单
### Description
本地请求支付订单，后台生成订单，返回支付订单信息。具体流程见下图。
![支付流程](http://www.dcloud.io/docs/a/payment/flow.png)

服务端生成支付宝订单示例
[link](https://github.com/dcloudio/H5P.Server/tree/master/payment)
### parameters
 name | required | type | note 
  --- | --- | --- | ---
 token | true | String | 令牌 
 type | true | Int | 支付类似，充值，支付账单，支付订单 
 id | true | String | 用户/账单/订单编号 
 channel | true | String | 支付通道，alipay,wxpay 
 amount | true | Double | 总金额 
 subject| true | String | 支付订单标题 
 body | false | String | 支付订单详情  
### Responses
返回支付订单信息

