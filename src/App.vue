<template>
  <Transition name="fade">
    <DetailModal
      :data="rooms"
      :selectedRoom="selectedRoom"
      v-if="isModalOpen == true"
      @closeModal="isModalOpen = false"
    />
  </Transition>

  <div class="menu">
    <a v-for="(item, index) in menu" :key="index">{{ item }}</a>
  </div>

  <!-- 할인배너 -->
  <DiscountBanner v-if="showDiscount" />

  <button @click="priceSort">가격순정렬</button>
  <button @click="priceRevSort">가격역순정렬</button>
  <button @click="textSort">가나다순정렬</button>
  <button @click="priceBelFiftySort">50만원 이하 상품 필터</button>

  <button @click="sortBack">초기화</button>

  <!-- 상품 -->
  <RoomCard
    v-for="(room, i) in rooms"
    :key="i"
    :data="room"
    @openModal="
      isModalOpen = true;
      selectedRoom = $event;
    "
  />
</template>

<!-- 데이터 바인딩 하는 이유 
1.하드코딩은 나중에 변경이 어려움 hardcoding is make hard data to modify later 
2. 실시간 자동 렌더링을 쓰기 위해 to use real timerendering
3. 애초에 바뀔일이 없으면 안해도 된다 
4.태그 속성 안에 데이터 바인딩 하고 싶으면 ;를 사용
<태그 v-for="작명 in 몇회 or 자료형">
-->

<script>
import data from './assets/data.js';
import DiscountBanner from './DiscountBanner.vue';
import DetailModal from './DetailModal.vue';
import RoomCard from './RoomCard.vue';

export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      roomsOriginal: [...data],
      selectedRoom: null,
      rooms: data,
      isModalOpen: false,
      countReport: [0, 0, 0],
      menu: ['Home', 'Shop', 'About'],
      customStyle: 'color:blue',
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
      imagePaths: [
        './assets/room0.jpg',
        './assets/room1.jpg',
        './assets/room2.jpg',
      ],
    };
  },
  methods: {
    increase(number) {
      this.countReport[number]++;
    },
    priceSort() {
      this.rooms.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    sortBack() {
      this.rooms = [...this.roomsOriginal];
    },
    priceRevSort() {
      this.rooms.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    textSort() {
      this.rooms.sort(function (a, b) {
        {
          return a.title.localeCompare(b.title);
        }
      });
    },
    priceBelFiftySort() {
      const sortedArray = this.rooms.filter((room) => room.price <= 500000);

      this.rooms = sortedArray;
    },
  },
  components: {
    DiscountBanner,
    DetailModal,
    RoomCard,
  },
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.roomImage {
  width: 90%;
  margin-top: 40px;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: 0.2s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: 0.2s;
}
.fade-leave-to {
  opacity: 0;
}
</style>
