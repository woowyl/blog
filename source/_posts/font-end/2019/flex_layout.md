---
title: Flex
date: 2019-03-03 14:05:05
categories: front-end
tags: 
- 前端
- 布局
---
## 容器上的六个属性
1. flex-direction
2. flex-wrap
   默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
<!-- more -->
```css
    .box {
     flex-wrap: nowrap | wrap | wrap-reverse;
     }
```
3. flex-flow
   flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
4. just-content
5. align-items
6. align-content

## 项目上的六个属性

1. order
  order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
2. flex-grow
3. flex-shrink
4. flex-basis
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
5. flex
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

6. align-self


