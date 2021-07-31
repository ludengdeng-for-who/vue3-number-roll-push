### 安装

```js
npm install vue-number-roll-plus --save

```

### 使用

#### 基本使用

```js
<template>
   <vue-number-roll-plus
      :number="9999"
      :isSemicolon="false"
      :speed="1"
      background="transparent"
    >
  </vue-number-roll-plus>
</template>

<script>
import VueNumberRollPlus from "vue3-number-roll-plus"
import "vue-number-roll-plus/main.css"
export default {
  components: {
    VueNumberRollPlus
  }
}
</script>
```

#### 属性

|    属性     |   属性含义   |     类型      | 默认值  |
| :---------: | :----------: | :-----------: | :-----: |
|   number    |  传入的数字  | Number/String |    0    |
| isSemicolon | 是否三位分隔 |    Boolean    |  true   |
|    speed    | 滚动速度(s)  |    Number     |    1    |
| background  |    背景色    |    String     | #0e68cc |

#### 事件

|    事件名    |      事件      |  参数  |
| :----------: | :------------: | :----: |
| numberChange | 数字变化后触发 | number |
