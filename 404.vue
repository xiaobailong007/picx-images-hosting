<template>
  <div class="notfound">
    <svg-icon name="404" />
    <div class="content">
      <h1>404</h1>
      <div class="desc">抱歉，你访问的页面不存在</div>
      <el-button type="primary" @click="goBack">{{ countdown }}秒后，返回首页</el-button>
    </div>
  </div>
</template>

<script lang="ts" setup>
interface StateTs {
  // eslint-disable-next-line no-undef
  inter: null | NodeJS.Timeout | number;
  countdown: number;
}

const state: StateTs = reactive({
  inter: 0,
  countdown: 5
});

const { inter, countdown } = toRefs(state);

const router = useRouter();

const goBack = () => {
  router.push("/");
};

inter.value = setInterval(() => {
  countdown.value--;
  if (countdown.value == 0) {
    clearInterval(Number(inter.value));
    goBack();
  }
}, 1000);
</script>

<style lang="scss" scoped>
.notfound {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  .svg-icon {
    height: 400px;
    width: 400px;
  }
  .content {
    h1 {
      margin: 0;
      font-size: 72px;
      color: #303133;
    }
    .desc {
      margin: 20px 0 30px;
      font-size: 20px;
      color: #606266;
    }
  }
}
</style>
