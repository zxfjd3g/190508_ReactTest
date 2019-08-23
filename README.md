## 0. git管理项目
    1). 创建本地仓库
        创建.gitignore配置文件
        git init
        git add *
        git commit -m "xxx"
    2). 创建远程仓库
        New Repository
        指定名称
        创建
    3). 将本地仓库推送到远程仓库
        git remote add origin https://github.com/zxfjd3g/xxx.git 关联远程仓库
        git push origin master
    4). 如果本地有更新, 推送到远程
        git add *
        git commit -m "xxx"
        git push origin master
    5). 如果远程有更新, 拉取到本地
        git pull origin master
    6). 克隆远程仓库到本地
        git clone https://github.com/zxfjd3g/xxx.git

## 1.1. React的基本认识
	1). Facebook开源的一个js库
	2). 一个用来动态构建用户界面的js库
	3). React的特点
		Declarative(声明式编码)
		Component-Based(组件化编码)
		Learn Once, Write Anywhere(支持客户端与服务器渲染)
		高效
		单向数据流
	4). React高效的原因
    	虚拟(virtual)DOM, 不总是直接操作DOM(批量更新, 减少更新的次数) 
    	高效的DOM Diff算法, 最小化页面重绘(减小页面更新的区域)

## 1.2. React的基本使用
	1). 导入相关js库文件(react.js, react-dom.js, babel.min.js)
	2). 编码:
		<div id="container"></div>
		<script type="text/babel">
			var aa = 123#  #
			var bb = 'test'
			ReactDOM.render(<h1 id={bb}>{aa}</h1>, containerDOM)
		</script>

## 1.3. JSX的理解和使用
	1). 理解
		* 全称: JavaScript XML
		* react定义的一种类似于XML的JS扩展语法: XML+JS
		* 作用: 用来创建react虚拟DOM(元素)对象
	2). 编码相关
		* js中直接可以套标签, 但标签要套js需要放在{}中
		* 在解析显示js数组时, 会自动遍历显示
		* 把数据的数组转换为标签的数组: 
			var liArr = dataArr.map(function(item, index){
				return <li key={index}>{item}</li>
			})
	3). 注意:
	    * 标签必须有结束
	    * 标签的class属性必须改为className属性
	    * 标签的style属性值必须为: {{color:'red', width:12}}


## 1.4. 几个重要概念理解
### 1). 模块与组件
	1. 模块:
	  	理解: 向外提供特定功能的js程序, 一般就是一个js文件
	  	为什么: js代码更多更复杂
	  	作用: 复用js, 简化js的编写, 提高js运行效率
	2. 组件: 
		理解: 用来实现特定界面功能效果的代码集合(html/css/js/img)
	  	为什么: 一个界面的功能太复杂了
	  	作用: 复用编码, 简化项目界面编码, 提高运行效率
### 2). 模块化与组件化
    1. 模块化:
    	当应用的js都以模块来编写的, 这个应用就是一个模块化的应用
    2. 组件化:
    	当应用是以多组件的方式实现功能, 这上应用就是一个组件化的应用

## 2.1. 组件基本理解和使用
	1). 自定义的标签: 组件类(函数)/标签
	2). 定义组件
		//方式1: 无状态函数(简单组件)
		function MyComponent1(props) {
			return <h1>自定义组件标题11111</h1>
		}
		//方式2: ES6类(复杂组件)
		class MyComponent3 extends React.Component {
			render () {
			  return <h1>自定义组件标题33333</h1>
			}
		}
	3). 渲染组件标签
		ReactDOM.render(<MyComp />,  cotainerEle)
	4). ReactDOM.render()渲染组件标签的基本流程
		React内部会创建组件实例对象/调用组件函数, 得到虚拟DOM对象
		将虚拟DOM并解析为真实DOM
		插入到指定的页面元素内部

## 2.2. 组件的3大属性: state
	1. 组件被称为"状态机", 页面的显示是根据组件的state属性的数据来显示
	2. 初始化指定:
        constructor() {
          super()
          this.state = {
            stateName1 : stateValue1,
            stateName2 : stateValue2
          }
        }
        state = {
            stateName1 : stateValue1,
            stateName2 : stateValue2
        }
	3. 读取显示: 
	    this.state.stateName1
	4. 更新状态-->更新界面 : 
	    this.setState({stateName1 : newValue})

## 2.2. 组件的3大属性: props
	包含所有组件标签的属性的集合对象
	在组件内部读取属性值(可能是函数): this.props.propertyName
	作用: 从目标组件外部向组件内部传递数据(只读)
	限制props的属性名/属性值类型/必要性
			Person.propTypes = {
				name: PropTypes.string.isRequired,
				age: PropTypes.number
			}
	限定props的属性默认值
			Person.defaultProps = {
				age: 18,
			}
	将对象的所有属性通过props传递
	    <Person {...person}/>

## 2.3. 组件的3大属性: refs
	是什么: 组件内包含ref属性的标签元素的集合对象
	作用: 找到组件内部的真实dom元素对象, 进而操作它
	使用方法(老的):
			给操作目标标签指定ref属性, 打一个名称标识
			获得标签对象: this.refs.refName
	使用方法(新的)
			1). 创建一个ref容器, 并保存到组件对象上
			2). 将ref容器交给要标识的标签, 内部就会将标签对象保存到ref容器中
			3). 通过ref容器的current属性得到标签对象

## 2.4. 组件中的事件处理
	1. 给标签添加属性: onXxx={this.eventHandler}
	2. 在组件中添加事件处理方法
	    eventHandler = (event) => {
	                
	    }
	3. 使自定义方法中的this为组件对象
	  	在constructor()中bind(this)
	  	使用箭头函数定义方法
	4. 如果想向事件回调函数传递特定参数
			onXxx={(event) => this.eventHandler(event, 'abc')}
	5. 事件监听
			绑定事件监听
				事件名
				回调函数
			触发事件
				事件名
				数据

## 2.5. 组件的组合使用
	1. 拆分组件: 拆分界面,抽取组件
	2. 实现静态组件: 使用组件实现静态页面效果
	3. 实现动态组件
			动态显示初始化数据
			交互功能(从绑定事件监听开始)