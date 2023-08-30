<template>
  <!-- 모달창 -->
  <div class="blackBg">
    <div class="whiteBg">
      <img style="width: 100%" :src="data[selectedRoom].image" />
      <h4>{{ data[selectedRoom].title }}</h4>
      <input v-model="month" />
      <p>{{ month }}개월 {{ data[selectedRoom].price * Number(month) }}원</p>
      <p>{{ data[selectedRoom].content }}</p>
      <button @click="$emit('closeModal')">close</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DetailModal',
  props: {
    data: Array,
    selectedRoom: Number,
  },
  data() {
    return {
      month: 1,
    };
  },

  updated() {
    if (this.month == 2) {
      alert('2는 입력 할 수 없습니다');
      this.month = 1;
    }
  },
};
</script>
<style>
.blackBg {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.whiteBg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>
