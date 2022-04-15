<template>
  <q-page class="flex flex-center">
    <div class="title">
      <img style="margin-top: 50px;width:100%"  src="/title.webp" alt="" srcset="" />
    </div>
    <div class="row" style="margin-top: -310px">
      <div class="col-12 flex flex-center" style="margin-bottom: 50px">
        <q-input
          v-model="iname"
          placeholder="请输入姓名"
          style="width: 40%"
        ></q-input>
      </div>
      <div class="col-12 flex flex-center">
        <q-btn
          @click="begin"
          style="
            background: #f0d044;
            color: #ff0000;
            font-weight: 900;
            font-size: 1.5rem;
            padding: 10px 40px;
            border-radius: 15px;
          "
          label="开始答题"
        />
      </div>
    </div>
    <span class="copy">NSITA-UED提供技术支持</span>
  </q-page>
</template>

<style>
.q-field__native {
  text-align: center !important;
  border-radius: 15px !important;
}
.copy{
  position: absolute;
  bottom: 10px;
  color: gray;
}
</style>
<script>
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "PageIndex",
  setup() {
    const iname = ref("");

    let router = useRouter();
    const begin = () => {
      if (iname.value == "") {
        alert("请输入姓名");
      } else {
        router.push({
          name: "dt",
          params: {
            name: iname.value,
          },
        });
      }
    };

    return { iname, begin };
  },
});
</script>
