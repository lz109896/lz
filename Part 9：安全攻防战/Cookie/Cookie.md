#### 1.	cookie 简介
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/cookie%20%E7%AE%80%E4%BB%8B%201png.png)
```
A: js 的变量可以保存信息，但是变量是有生命周期的，一旦页面刷新，包括全局变量在内的所有变量都会销毁，所以变量没法保存持久
化的信息。而 cookie 实际上是在保存在浏览器本地的信息，它们储存的信息会保存在本地文件中，就算页面刷新了，信息也还是存在。

B: 我们可以通过 Expires 字段设置 cookie 过期时间，设置了过期时间的 cookie 就是持久化 cookie， 只有超过
过期时间cookie才会失效，关闭浏览器并不会使持久化 cookie 失效，B选项不对

C: 没有设置过期时间的 cookie，就是我们说的临时 cookie 的定义，关闭浏览器后就会失效

D: cookie 虽然可以储存本地信息，但是不适合储存大量的信息，因为 cookie 还有个特点是每次请求都会带上这个域相关的所有 
cookie，就是说，cookie 会影响浏览器请求的大小，因此我们要尽量保持 cookie 体积小，还有尽量用于保存跟用户相关的信息。
同时，浏览器本身对 cookie 总大小也有限制，目前是不允许超过 4k，超过的会丢失。

```
#### 2.	js 操作 cookie

document.cookie  拿cookie
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20%E6%93%8D%E4%BD%9C%20cookie%201.png)
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20%E6%93%8D%E4%BD%9C%20cookie%202.png)
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20%E6%93%8D%E4%BD%9C%20cookie%203.png)

##### 第三方库操作，不要直接使用，要将原生的接口操作一遍
![]()

#### 3.	js cookie 操作实战

Session :的意思是临时cookie 关闭浏览器 cookie 就消失了

读 cookie （拿cookie）
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%201.png)

增加 cookie 
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%202.png)

domain 只能设置你的域名上一级，比如四级的，只能设置为3级
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%203.png)

设置'path=/' 全站都可以访问

![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%204.png)

删除 cookie （过期时间，经常使用的是expires）

![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%205.png)

固化（持久化） cookie 只需要设置 expires 设置的时间是未来的时间就可以了
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/js%20cookie%20%E6%93%8D%E4%BD%9C%E5%AE%9E%E6%88%98%206.png)


#### 4.	使用 cookie 保存用户信息
```
HTTP 是无状态的协议：谁来访问分不出来

登录和注销都是通过 cookie 来协商浏览器端和服务器端
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/%E4%BD%BF%E7%94%A8%20cookie%20%E4%BF%9D%E5%AD%98%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF%201.png)
![](https://raw.githubusercontent.com/lz109896/Web-datum/34db94675a2e7d396ea70af2e5aa96dc1eb92ac3/%E4%BD%BF%E7%94%A8%20cookie%20%E4%BF%9D%E5%AD%98%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF%202.png)

#### 5.	cookie 实现登录演示
```
1.git clone 克隆项目到本地
2.执行 npm install 一下安装下依赖包
3.执行 $ node index   启动服务

```
