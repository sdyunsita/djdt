<template>
  <q-page class="flex flex-center">
    <div class="title" style="visibility:hidden">
      <img alt="" src="/title.webp" srcset="" style="margin-top: 50px;width:100%"/>
    </div>
    <div class="row" style="margin-top: -310px">
      <div class="col-12 flex flex-center" style="margin-bottom: 2rem">
        <q-input
          v-model="iname"
          placeholder="请输入姓名"
          style="width: 40%"
        ></q-input>
      </div>
      <div class="col-12 flex flex-center">
        <q-btn
          label="开始答题"
          style="
            background: #f0d044;
            color: #ff0000;
            font-weight: 900;
            font-size: 1.5rem;
            padding: 10px 40px;
            border-radius: 15px;
          "
          @click="begin"
        />
      </div>
    </div>
    <span class="copy">
      <div>信息工程学院</div>NSITA-UED提供技术支持</span>
  </q-page>
</template>

<style>
.q-field__native {
  text-align: center !important;
  border-radius: 15px !important;
}
</style>
<style lang="scss" scoped>

.copy {
  position: absolute;
  bottom: 10px;
  color: gray;
  text-align: center;

  div {
    font-size: 1.5rem;
    color: black;
  }
}
</style>
<script>
import {defineComponent, ref} from "vue";
import {useRouter} from "vue-router";
import {api} from 'boot/axios'

export default defineComponent({
  name: "PageIndex",
  setup() {
    const iname = ref("");

    //日期判断
    const time = ref('')
    const m = ref('')
    api.get("https://api.m.jd.com/client.action?functionId=queryMaterialProducts&client=wh5").then((res) => {
      time.value = res['data']['currentTime'].slice(8,10)
      // time.value = 20
      // m.value = 5
      m.value = res['data']['currentTime'].slice(6, 7)
    });
    let router = useRouter();
    const begin = () => {
        if (iname.value == "") {
          alert("请输入姓名");
        } else {
          if ((m.value < 4) || !(time.value < 21)) {
            alert("未到活动开始时间")
          } else {
            router.push({
              name: "dt",
              params: {
                name: iname.value,
              },
            });
          }
        }
      }
    ;

    return {iname, begin};
  },
});
</script>
