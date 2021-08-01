<template>
  <div>
    <div
      v-for="(item, index) in computedNumber"
      :key="index"
      class="real-time-num"
      :style="{ background: background }"
    >
      <div
        class="real-time-num-item"
        :style="{
          transform:
            item !== ','
              ? `translateY(-${item * 40}px)`
              : `translateY(-${10 * 40}px)`,
          transition: `all ${speed}s ease-out`,
        }"
      >
        <div>0</div>
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
        <div>,</div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs, watch, defineComponent} from "vue";
export default defineComponent({
  props: {
    number: {
      type: [Number, String],
      default: 0,
    },
    isSemicolon: {
      type: Boolean,
      default: false,
    },
    speed: {
      type: Number,
      default: 1,
    },
    background: {
      type: String,
      default: "#0e68cc",
    },
  },
  emits: ["numberChange", "done"],
  setup(props, ctx) {
    let obj = reactive({
      computedNumber: [],
    });
    initPage();
    setTimeout(() => {
      ctx.emit("done", props.number);
    }, props.speed * 1000);
    watch(
      () => props.number,
      (val) => {
        initPage();
        ctx.emit("numberChange", val);
        setTimeout(() => {
          ctx.emit("done", val);
        }, props.speed * 1000);
      }
    );
    function string2List(str) {
      const list = [];
      const res = [...String(str)].reverse();
      let currentIndex = 1;
      res.forEach((item, index) => {
        list.push(item);
        currentIndex++;
        if (props.isSemicolon) {
          if (currentIndex === 4 && index != res.length - 1) {
            list.push(",");
            currentIndex = 1;
          }
        }
      });
      list.reverse();
      return list;
    }
    function setComputedList() {
      obj.computedNumber = [];
      string2List(props.number).forEach(() => {
        obj.computedNumber.push(0);
      });
    }
    function initPage() {
      setComputedList();
      setTimeout(() => {
        obj.computedNumber = string2List(props.number);
      });
    }
    return {
      ...toRefs(obj),
    };
  },
});
</script>

<style scoped>
.real-time-num {
  display: inline-block;
  width: 30px;
  height: 40px;
  line-height: 40px;
  margin-left: 3px;
  overflow: hidden;
  text-align: center;
}

.real-time-num > div {
  /* width: 30px;
    height: 40px; */
}
</style>