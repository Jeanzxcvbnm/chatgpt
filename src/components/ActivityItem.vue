<template>
  <van-card class="activity-item">
    <img class="img" slot="thumb" :src="activity.image" />
    {{ activity }}
    <div class="activity-info">
      <h2>{{ activity.title }}</h2>
      <p>{{ activity.description }}</p>
      <van-tag>￥{{ activity.price }}</van-tag>
    </div>
  </van-card>
</template>
<script>
import { Card, Tag } from "vant";

export default {
  components: {
    Card,
    Tag,
  },
  props: {
    activity: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>
<style scoped lang="less">
.activity-item {
  display: flex;
  .img {
    width: 88px;
    height: 88px;
  }
}

.activity-info {
  padding: 20px;
}

h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

p {
  color: gray;
}
</style>
