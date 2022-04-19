<template>
  <q-page class="flex flex-center">
    <img style="width: 328px; height: 178px;visibility: hidden" src="/result.webp" />
    <div class="main">
      <div class="info">
        <div class="cc">
          {{ name }} 同学，祝贺您在<br>“悦动校园跑“--红色教育答题站<br>取得优异成绩！
        </div>
        <div class="ss">得分:{{ score }}<br />用时:{{ time }}</div>
      </div>
    </div>
    <div class="xy">
     信息工程学院
      <div class="txt">请截图保存此页面以作为参加依据</div>
    </div>
  </q-page>
</template>
<style lang="scss" scoped>
img {
  position: absolute;
  top: 11vh;
}
.main {
  text-align: center;
  position: absolute;
  width: 80%;
  bottom: 22%;
  .info {
    color: #6a685c;
    font-size: 1.5rem;
    font-weight: 600;
    .cc {
      margin-bottom: 4vh;
    }
    .ss{
      color: red;
    }
  }
}
.xy {
  position: absolute;
  bottom: 5vh;
  font-size: 1.5rem;
  text-align: center;
  .txt {
    font-size: 1rem;
    color: gray;
  }
}
</style>
<script>
import { useRoute, useRouter } from "vue-router";
import { onMounted, ref } from "vue";
import router from "src/router";
export default {
  setup(props, ctx) {
    //router是全局路由对象，route= userRoute()是当前路由对象
    let route = useRoute();
    const name = route.params.name;
    const score = route.params.score;
    const time = route.params.time;
    let router = useRouter();
    onMounted(() => {
      console.log(score);
      if (typeof score == "undefined") {
        router.push("/");
      }
    });
    return {
      name,
      score,
      time,
    };
  },
};
</script>
