---
id: vtwqYuxNQHvKl9mrbEp58
title: Element Plus踩坑
desc: ''
updated: 1644395068961
created: 1644394952475
---

1. element-plus版本1.3.0beta1  
   1. formModel要使用:model绑定
   2. 需要在form-item上添加prop属性，并设置为formModel中的字段
   3. input等组件，需要用v-model绑定数据
