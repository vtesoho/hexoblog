---
title: Hooks学习第一章
date: 2020-1-03 16:51:24
comments: true #是否可评论
toc: true #是否显示文章目录
categories: "React" #分类
tags:   #标签
	- react
---

hooks是react新加入的一个特性，非常好用。直接进入正题。

我们正常的建立计数器组件是采用这种方式

```js
class MyCount extends React.Component{
    state = {
        count: 0
    }

    componentDidMount(){
        this.interval = setInterval(()=> {
            this.setState({count:this.state.count + 1})
        },1000)
    }

    componentWillMount(){
        if(this.interval){
            clearInterval(this.interval)
        }
    }

    render(){
        return <span>{this.state.count}</span>
    }
}
```

然后我们采用hooks的方式来建立
```js
import React,{useState,useEffect} from 'react'
function MyCountFunc(){
    const [count,setCount] = useState(0)

    useEffect(()=> {
        const interval = setInterval(()=> {
            setCount(c => c + 1)
        },1000)

        return () => clearInterval(interval)
    },[])


    return <span>{count}</span>
}
```

可以看到多引用了二个方法，useState和useEffect，useState就相当于在state里面创建了一个变量和修改的方法，useEffect这里面的代码相当于是在componentDidMount的生命周期去执行，这里面return是相当于componentWillMount的时候去执行。

二者相对比发现，采用hooks方式写的代码简洁很多，这只是hooks学习的第一步，现在去更深层次的学习hooks吧。


