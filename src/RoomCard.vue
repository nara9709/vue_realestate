<template>
  <div>
    <img class="roomImage" :src="data.image" />
    <h4 @click="$emit('openModal', data.id)">{{ data.title }}</h4>
    <p>{{ data.price }}원</p>
  </div>
</template>
<script>
export default {
  props: {
    data: Object,
  },
};
</script>
<style></style>
