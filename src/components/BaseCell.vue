<template>
  <div class="cell" @click="shot">
    {{ marker }}
    <!-- استخدم marker مباشرةً من الـ props -->
  </div>
</template>

<script>
import EventBus from "@/EventBus";

export default {
  name: "BaseCell",
  props: ["marker"], // marker هو الـ prop الذي يتم تمريره من BaseGrid
  data() {
    return {
      canPlaceMark: true, // تحديد ما إذا كانت الخلية قابلة لتخزين علامة
    };
  },
  methods: {
    shot() {
      // تأكد من أن الخلية لم يتم استخدامها بالفعل
      if (this.canPlaceMark && this.marker === "") {
        // تأكد من أن الـ marker فارغ
        this.canPlaceMark = false; // إغلاق الخلية بعد وضع العلامة
        EventBus.$emit("shot", this.marker); // إرسال الحدث
      }
    },
  },
};
</script>

<style scoped>
.cell {
  height: 120px;
  line-height: 120px;
  font-size: 3.5em;
  background-color: lightblue;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
}

.cell:hover {
  background-color: aquamarine;
  cursor: pointer;
}
</style>
