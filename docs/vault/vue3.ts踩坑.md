---
id: 0yy4b0CipIejbDM53wVzG
title: TS踩坑
desc: ""
updated: 1644546905779
created: 1644488968460
---

1. 如何用 vue + ts 注册全局方法 [参考文档](https://https://v3.cn.vuejs.org/guide/typescript-support.html#%E4%B8%8E-options-api-%E4%B8%80%E8%B5%B7%E4%BD%BF%E7%94%A8)
   1. 插件法（推荐）

```typescript
        export const foo = {
            console.log("foo");
        }
        // main.ts中引入
        import {foo} from '@/util/utils';
        app.config.globalProperties.$foo = foo;

        // 添加类型声明 xx.d.ts
        import foo from '@/util/foo';
        declare module '@vue/runtime-core' {
            export interface ComponentCustomProperties {
                $foo: Function;
            }
        }
```

```vue
        // 页面使用
        <template>{{ $foo() }}</template>
```
