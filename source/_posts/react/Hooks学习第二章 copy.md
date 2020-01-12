---
title: Hooks学习第二章
date: 2020-1-03 17:49:52
comments: true #是否可评论
toc: true #是否显示文章目录
categories: "React" #分类
tags:   #标签
	- react
---

前面已经简单的写了一个hooks的demo，了解了hooks的基本用法，这一章介绍一下useState，和useReducer，先看看useState。

```js
import React,{useState} from 'react'
function MyCountFunc(){
    const [count,setCount] = useState(0)

    setCount(1)   //直接设置一个新的值
    setCount((c) => c+1)  //这里的c是在setCount执行的时候取到最新的count的值

    return <span>{count}</span>
}
```

在来看看useReducer，useReducer一般是用在比较复杂的对象里面。useState其实也是一个useReducer。

```js
import React,{useReducer} from 'react'

function countReducer(state,action){
    switch (action.type){
        case 'add':
            return state + 1
        case 'minus':
            return state - 1
        default:
            return state
    }
}

function MyCountFunc(){
    const [count,dispatchCount] = useReducer(countReducer,0)

    useEffect(()=> {
        const interval = setInterval(()=> {
            dispatchCount({type: 'add'})
        },1000)
        return () => clearInterval(interval)
    },[])

    return <span>{count}</span>
}
```


useEffect
```js
//useEffect 的第二个参数作用是设置的这个值有变化才会执行第一个参数里面的回调
//react官网上建议是只要你在方法里面用到的依赖，就必须放到第二个参数里
// 会在dom更新后回执行回调
useEffect(()=>{
    // console.log('effect invoked')
    console.log(inputRef)
    return () => console.log('effect deteched')
    
},[name,testarray])



// useLayouteffect 会在dom更新前执行回调
// 建议少用useLayoutEffect，因为是在dom更新前执行，如果执行时间过长，会影响dom的渲染。
useLayoutEffect(()=>{
    console.log('useLayoutEffect invoked')
    return () => console.log('useLayoutEffect deteched')
},[name,testarray])
```