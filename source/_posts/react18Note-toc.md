---
title: react 18 笔记目录
author: 菜鸟书生
banner:
  type: img
  bgurl: https://pic1.zhimg.com/v2-b3c2c6745b9421a13a3c4706b19223b3_r.jpg
  bannerText: 入门React
categories:
  - react
tags:
  - react
  - note
date: 2023-04-25 23:41:45
keywords: 
toc: true
---

# React18核心概念与类组件使用

## props细节详解及注意事项
### 构造器中获取props数据
### 多属性的传递
### 给属性添加默认值与类型

## 类组件中事件的使用详解
### 事件中this的处理
### 事件传参处理

## state细节详解及React18的自动批处理
### 自动批处理
### 异步处理

## PureComponent与shouldComponentUpdate
### shouldComponentUpdate
### PureComponent

## immutable.js不可变数据集合
### immutable.js库

## Refs操作DOM及操作类组件
### React.createRef()
### 回调函数写法
### Ref操作类组件

## 详解常见生命周期钩子函数

## 详解不常见生命周期钩子函数

## getDerivedStateFromProps
### shouldComponentUpdate
### getSnapshotBeforeUpdate

## 组件内容的组合模式

## 复用组件功能之Render Props模式
### Render Props模式

## 复用组件功能之HOC高阶组件模式
### HOC高阶组件

## 组件跨层级通信方案Context
### Context通信

# React18之Hook与函数组件 – 优雅简易的开发模式 

## 函数组件基本使用及点标记组件写法
### 函数组件的基本使用
### 点标记组件写法

## Hook概念及Hook之useState函数
### 什么是Hook

## 详解Hook之useEffect函数
### 什么是useEffect Hook
### 使用多个 Effect 实现关注点分离
### 通过跳过 Effect 进行性能优化
### Effect 中使用了某个响应式数据，一定要进行数组的依赖处理
### 频繁的修改某个响应式数据，可通过回调函数进行改写
### useEffect异步与useLayoutEffect同步

## 详解Hook之useRef函数
### 回调函数形式
### useRef()形式
### 函数转发
### useRef的记忆能力

## 详解Hook之useContext函数
### useContext函数

## 函数组件性能优化之React.memo

## 详解Hook之useCallback与useMemo函数

## 详解Hook之useReducer函数

## React18之并发模式与startTransition

## React18之useTransition与useDeferredValue
### useTransition
### useDeferredValue

## 函数组件功能复用之自定义Hook

# React18扩展内容与脚手架使用 – 全面掌握React18特性 

## 脚手架安装及vsCode插件安装
### 脚手架的安装
### 插件的安装
### 脚手架下需要注意的点

## 脚手架下样式处理方式及Sass支持
### 全局样式
### 预编译CSS的支持
### 模块化CSS
### CSS-in-JS
### 样式模块classnames

## Ant Design框架的安装与使用（一）
### 什么是Ant Design框架

## Ant Design框架的安装与使用（二）
### 逻辑组件

## 仿Ant Design的Rate组件实现

## 仿Ant Design的Button组件实现

## react-transition-group模块实现动画功能
### react-transition-group模块


## createPortal传送门与逻辑组件的实现
### createPortal传送门

## React.lazy与React.Suspense与错误边界
### React.lazy与React.Suspense
### 错误边界

# ReactRouter路由与Redux状态管理 – 组织与架构应用

## ReactRouterV6.4 基础路由搭建
### 路由的安装

## 动态路由模式与编程式路由模式
### 动态路由模式
### 带样式的声明式路由NavLink
### 编程式路由

## useSearchParams与useLocation函数

### useLocation函数
### useSearchParams函数

## 默认路由展示与重定向路由与404处理
### 默认路由
### 重定向路由
### 处理404页面

## 路由loader函数与redirect方法

### loader函数
### redirect方法

## 自定义全局守卫与自定义元信息
### 自定义全局守卫
### 自定义元信息

## Redux状态管理的基本流程
### Redux状态管理库

## react-redux简化对Redux的使用
### react-redux库

## 如何处理多个reducer函数及Redux模块化
### 模块化Redux

## redux-thunk中间件处理异步操作
### redux-thunk中间件


## Redux-Toolkit(RTK)改善Redux使用体验
### Redux-Toolkit(RTK)库

## Redux-Toolkit(RTK)如何处理异步任务

### createAsyncThunk方法

##  通过redux-persist进行数据持久化处理

### redux-persist模块

## 路由加状态管理的登录拦截综合案例
## 类组件中如何使用路由和状态管理



