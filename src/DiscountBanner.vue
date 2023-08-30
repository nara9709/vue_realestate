<template>
  <div class="discount">
    <h4>지금 결제하면 {{ this.discount }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'DiscountBanner',
  data() {
    return {
      discount: 20,
    };
  },

  mounted() {
    return (this.interval = setInterval(() => {
      this.discount = this.discount - 1;
    }, 500));
  },

  updated() {
    if (this.discount == 0) {
      console.log('thisiszero');
      clearInterval(this.interval);
      this.interval = undefined;
    }
  },
};
</script>
<style>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
