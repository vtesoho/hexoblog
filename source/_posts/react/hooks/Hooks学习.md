---
title: Hooks学习
date: 2020-1-07 15:49:24
comments: true #是否可评论
toc: true #是否显示文章目录
categories: "React" #分类
tags:   #标签
	- react
---


# hooks

### 基本用法对比
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

// --------------------------

import React,{useState,useEffect} from 'react'
function MyCountFunc(){
    const [count,setCount] = useState(0)


    //useEffect会在组件执行完更新的时候执行
    useEffect(()=> {
        const interval = setInterval(()=> {
            setCount(c => c + 1)
        },1000)
        return () => clearInterval(interval)    //return会在组件被卸载的时候去执行
    },[])


    return <span>{count}</span>
}
```


1. useState
```js
import React,{useState} from 'react'
function MyCountFunc(){
    const [count,setCount] = useState(0)

    setCount(1)   //直接设置一个新的值
    setCount((c) => c+1)  //这里的c是在setCount执行的时候取到最新的count的值

    return <span>{count}</span>
}
```
2. useEffect
3. useReducer
4. useContext
5. useRef
6. useMoon

