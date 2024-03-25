# matr1x 脚本环境安


https://matr1x.io/max-even

自用脚本，有需要关注公众号：韭阳真经，然后上面有微信，价格公道



## 1.python环境安装



参考链接：https://zhuanlan.zhihu.com/p/397160941

## 2.redis环境安装教程

参考链接：https://developer.aliyun.com/article/1347971

## 3.脚本使用教程

#### 3.1 环境配置和导包

- 第一步，配置redis环境

  打开config目录，找到config.py，用编辑器修改里面配置文件：

  本机跑如果上一步没设置redis密码就跳过这一步

  ~~~
  # redis配置 -*- coding: utf-8 -*-
  redis_web3_host = 'localhost'
  redis_web3_port = 6379
  redis_web3_db = 0
  redis_web3_password = ''
  ~~~
  
- 第二步：配置最大要是claim数量（针对想要省gas用户一天最多claim三次，如果想取消限制该为零）
  
~~~
  # 这个数量根据你每日现在最大claim key次数，如果为0 默认最大次数
  num_key = 3
~~~

- 自定义邀请码配置（非必填）
  
~~~
  # 这个填你默认的邀请码，没有会从这里取，后面默认会从你主钱包账号自动提取邀请码
  own_code = ['code1','code2']
  
  
~~~
- **程序gas不足时自动转账配置（必填）**
~~~
这一块一定要去配置，当程序交互时候遇到gas不足时候，会自动从配置的钱包里面随机取个钱包转账，转账金额从当前配置范围随机取
trigger_balance：每次程序运行会去检测账户余额是不是小于这个值，如果小于就会从wallets/tranf_wallets/from_wallets.txt里面随机取个钱包转账
转账金额范围为min_tranf_num-max_tranf_num之间随机一个金额，一定要配置，金额范围根据实际来


# 设置触发转账的余额阈值，账户余额低于该值开始转账，默认余额低于0.03 马蹄自动转账
trigger_balance = 0.03
# gas不足时候自动转账余额最小值（在最小到最大值之间随机），默认最小0.5马蹄
min_tranf_num = 0.5
# gas不足时候自动转账余额最大值，默认最大1.5马蹄
max_tranf_num = 1.5



~~~



- 网站交互代理配置（代理获取见下面《动态代理使用》目录）
  
~~~
  #该代理仅用于交互网站 不用于绑定推特，推特任务走每个推特账号对应的代理，默认为[]即交互不使用代理
  #配置示例proxy = ["8dtio2pg:AeIC909jnals39@24.144.71.110:3112"]
  #如果你自己有多条ip代理，也可以配置,至少5条再用proxy = ["user:pwd@ip1:port","user:pwd@ip2:port","user:pwd@ip3:port"]
  proxy=[]
~~~

- 导包：命令终端输入'pip3 install -r requirements.txt'导包

## 4.程序使用教程：

#### 4.1不绑定推特只进行邀请任务

	将你的私钥和地址以address,privatekey格式保存在wallets/sign_wallets/sign.txt里面 ，注意地址和私钥以英文逗号分隔
	
	然后再pycharm运行main.py即可
	
	程序会自动提取邀请码注册，自动完成任务

#### 4.2绑定推特进行全部任务

	将你的私钥和地址、推特token、静态代理ip以address,privatekey,twitter_token,proxy_ip格式保存在wallets/sign_wallets/sign_tw_ip.txt里面 ，注意以英文逗号分隔
	
	然后再pycharm运行main_tw.py即可
	
	程序会自动提取邀请码注册，自动授权推特进行转发评论点赞等任务

#### 4.3自动提取已经注册账号邀请码

	建议运行上面两个程序之前先运行get_code.py  将你所有需要提取邀请码的账户放在sign.txt，格式：address,privatekey
	
	然后运行即可

#### 4.4服务器全天24小时自动运行

	默认每天运行五次，如果超过五次会在第二天早上10点以后再次运行五次
	
	在pycharm运行main_job.py或者main_tw_job.py或者在命令行运行 python main_job.py 每天会自动运行
	
	如果是linux服务器直接执行：nohup python main_job.py > main.out & 或者nohup python main_job.py > main_tw_job.out &即可自动运行

4.动态代理使用（http代理）

默认使用代理官网https://app.proxy-cheap.com/r/TzQQJu：

点进去：![uxw1Go](https://raw.githubusercontent.com/91qkxs/tc/file/uPic/uxw1Go.png)



然后注册登录完最终选择这个购买

4.99美金可以买 1G，1G应该可以用很长时间，当然号越多消耗越大，

买了之后，在我的代理页面

![iOEdEw](https://raw.githubusercontent.com/91qkxs/tc/file/uPic/iOEdEw.png)

点击凭证生成器里面***设置凭证***，

![LcdUJQ](https://raw.githubusercontent.com/91qkxs/tc/file/uPic/LcdUJQ.png)

按照我这样 点击生成，上面选择1,将生成完的下面证书复制到脚本config目录下面config.py即可

![unPEmZ](https://raw.githubusercontent.com/91qkxs/tc/file/uPic/unPEmZ.png)