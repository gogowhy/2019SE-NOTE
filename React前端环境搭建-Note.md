# React前端环境搭建-Note
## 1.React 环境配置
### visual studio code安装
### node.js安装
1.nodejs长期支持版本
2.npm install +【需要的组件的名】
3.使用npm install ，nodejs根据package.json文件的依赖自动下载
### yarn安装
在a前端开发中更喜欢使用yarn命令来下载组建，当系统提示无法加载组建的时候通过yarn add+【组建名】 即可将组件安装到电脑上
### react 安装
#### 1.安装
使用npm 进行react安装 也可以使用淘宝镜像
npm install -g cpm —registry=https://registry.npm.taobao.org
#### 2.新建react项目
cpm install -g crest-react-app
create-react-app {文件名 不需要加花括号}
cd my-app
npm start
打开http：localhost3030，即可
## 2.关于前端的css
ant-design兼容react解决前端css
[Ant Design - A UI Design Language](https://ant.design/index-cn)
## 前端环境常见问题：
### 页面跳转问题
目前解决办法：
1.使用router 新建一个js文件，

````javascript
class App extends React.Component {
render(){
return(
<Router >
<div>
<Route exact path="/" component={Navi} />
<Route path="/Login" component={Login} />
<Route path="/register" component={register} />
<Route path="/cart" component={cart}/>
<Route path="/bookview" component={bookview}/>
<Route path="/order" component={order}/>

</div>
</Router>
)
}
}
export default App;

````
将需要链接的js链接到一个js文件中 ，
````javascript
import App from './App';
ReactDOM.render(<App />, document.getElementById('root'));
````
在接口引入这个js文件，在需要的js中import link，然后使用link to 语句即可。 参考网页：[React学习及实例开发（三）——用react-router跳转页面 - 麦豇豆 - 博客园](https://www.cnblogs.com/MaiJiangDou/p/9245063.html)



