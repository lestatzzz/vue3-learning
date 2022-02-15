---
id: vtwqYuxNQHvKl9mrbEp58
title: Element Plus踩坑
desc: ''
updated: 1644817659777
created: 1644394952475
---

# element-plus版本1.3.0beta1  

   1. formModel要使用:model绑定
   2. 需要在form-item上添加prop属性，并设置为formModel中的字段
   3. input等组件，需要用v-model绑定数据

## 如何在同一个formItem里校验多个select  

   使用嵌套formItem来解决，最外层的formItem的prop设置为第一个需要校验的formItem的prop  
   formRules里就正常定义需要校验的formModel的属性

```html
  <el-form-item label="预测颗粒度" prop="forecastDimensionTime">
      <el-form-item :rules="formRules.forecastDimensionTime" prop="forecastDimensionTime">
          <el-select v-model="formModel.forecastDimensionTime" placeholder="请选择时间" class="w-select">
              <el-option v-for="item of timeDimension.list" :key="item.code" :value="item.code" :label="item.name"></el-option>
          </el-select>
      </el-form-item>
      <el-form-item :rules="formRules.forecastDimensionSku" prop="forecastDimensionSku">
          <el-select v-model="formModel.forecastDimensionSku" placeholder="请选择商品" class="w-select">
              <el-option v-for="item of goodsDimension.list" :key="item.code" :value="item.code" :label="item.name"></el-option>
          </el-select>
      </el-form-item>
      <el-form-item :rules="formRules.forecastDimensionLocate" prop="forecastDimensionLocate">
          <el-select v-model="formModel.forecastDimensionLocate" placeholder="请选择地点" class="w-select">
              <el-option v-for="item of siteDimension.list" :key="item.code" :value="item.code" :label="item.name"></el-option>
          </el-select>
      </el-form-item>
  </el-form-item>
```

```typescript
   const formRules = reactive({
  forecastDimensionTime: [
    {
      required: true,
      message: "请选择预测颗粒度",
      trigger: "change",
    },
  ],
  forecastDimensionSku: [
    {
      required: true,
      message: "请选择预测颗粒度",
      trigger: "change",
    },
  ],
  forecastDimensionLocate: [
    {
      required: true,
      message: "请选择预测颗粒度",
      trigger: "change",
    },
  ],
});
```

   对出现在drawer里的form表单，在drawer关闭时应当清空已填入或选择的数据和校验规则（dialog同理）

```typescript
const onCancel = (formEl: InstanceType<typeof ElForm> | undefined) => {
   visible.value = false;
   drawerStore.initialize();
   nextTick(() => {
      formEl.clearValidate();
   });
};
```
