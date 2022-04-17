<template>
  <div class="content">
    <template v-if="typeof currentdata.data.title != '题目'">
      <div class="title">
        {{ currentdata.data.title }}
      </div>
      <div
        v-for="(value, index) in currentdata.data.option"
        :key="index"
        class="op"
      >
        <div
          v-for="(v, k) in value"
          :key="k"
          :class="{ Selectedcss: select == k }"
          class="opt"
          @click="selected(k)"
        >
          {{ k }}:{{ v }}
        </div>
      </div>
    </template>
    <div class="row abtn">
      <q-btn v-show="currentid != 0" class="col q-mr-lg bbtn" @click="foward"
      >上一题
      </q-btn
      >
      <q-btn
        v-show="currentid != data.length - 1"
        class="col bbtn"
        @click="next"
      >下一题
      </q-btn
      >
      <q-btn
        v-show="currentid == data.length - 1"
        class="col bbtn"
        style="color: #f0d044"
        @click="end"
      >结束答题
      </q-btn
      >
    </div>
  </div>
</template>

<style lang="scss" scoped>
.Selectedcss {
  background-color: rgba(255, 0, 0, 1) !important;
  color: white !important;
}

.content {
  min-height: 80vh;
  background: rgba(239.99999999999997, 208, 67.99999999999999, 1);
  border-radius: 15px;
  position: absolute;
  width: 90%;
  left: 50%;
  transform: translateX(-50%);
  top: 10%;
  padding: 20px;
  font-size: 1rem;

  .title {
    background-color: white;
    border-radius: 15px;
    min-height: 10vh;
    padding: 20px;
  }

  .op {
    .opt {
      background-color: white;
      border-radius: 15px;
      padding: 10px 20px;
      margin: 10px 0px;
    }
  }

  .abtn {
    position: absolute;
    width: 85%;
    left: 50%;
    transform: translateX(-50%);
    bottom: 20px;

    .bbtn {
      width: 100%;
      background-color: rgba(255, 0, 0, 1);
      color: white;
      letter-spacing: 2px;
      font-size: 1rem;
      font-weight: 500;
    }
  }
}
</style>
<script>
import {onMounted, reactive, ref} from "vue";
import {useRouter, useRoute} from "vue-router";

export default {
  name: "dati",
  props: {},
  setup() {
    //接收值
    let route = useRoute();
    const sname = route.params.name;

    const data = [
      {
        title:
          "第一题：党准确把握世界范围内思想文化相互激荡、我国社会思想观念深刻变化的趋势，强调意识形态工作是为国家立心、为民族立魂的工作，_____是更基础、更广泛、更深厚的自信，是一个国家、一个民族发展中最基本、最深沉、最持久的力量。",
        option: [
          {A: "道路自信"},
          {B: "制度自信"},
          {C: "理论自信"},
          {D: "文化自信"},
        ],
        anwser: "RA==",
      },
      {
        title:
          "第二题：党确立习近平同志党中央的核心、全党的核心地位，确立习近平新时代中国特色社会主义思想的指导地位，反映了全党全军全国各族人民共同心愿，对新时代党和国家事业发展、对推进中华民族伟大复兴历史进程具有_____。",
        option: [
          {A: "基础性意义"},
          {B: "关键性意义"},
          {C: "决定性意义"},
          {D: "发展性意义"},
        ],
        anwser: "Qw==",
      },
      {
        title:
          "第三题：一九七八年十二月，党召开_____，果断结束“以阶级斗争为纲”，实现党和国家工作中心战略转移，开启了改革开放和社会主义现代化建设新时期，实现了新中国成立以来党的历史上具有深远意义的伟大转折。",
        option: [
          {A: "十一届一中全会"},
          {B: "十一届二中全会"},
          {C: "十一届三中全会"},
          {D: "十一届四中全会"},
        ],
        anwser: "Qw==",
      },
      {
        title:
          "第四题：习近平总书记在北京大学师生座谈会上发表重要讲话并强调，要坚持不懈培育和弘扬社会主义核心价值观，引导广大师生做社会主义核心价值观的_____。",
        option: [
          {A: "坚定信仰者"},
          {B: "积极传播者"},
          {C: "模范践行着"},
          {D: "以上都对"},
        ],
        anwser: "RA==",
      },
      {
        title:
          "第五题：习近平总书记在中国政法大学参加“不忘初心跟党走”主题团日活动时深刻指出，共青团是党的助手和后备军，要始终保持先进性，广大团员青年_____,就是初心。不忘这个初心，是我国广大青年的政治选择，也是我国广大青年的人生航向。",
        option: [
          {A: "坚定跟党走"},
          {B: "积极上进"},
          {C: "学习成才"},
          {D: "服务社会"},
        ],
        anwser: "QQ==",
      },
      {
        title: "第六题：新时代中国青年运动的时代主题是_____。",
        option: [
          {A: "为实现中华民族伟大复兴的中国梦而奋斗"},
          {B: "为中华之崛起而读书"},
          {C: "为提高中国国际地位而努力"},
          {D: "为生态保护而奉献"},
        ],
        anwser: "QQ==",
      },
      {
        title:
          "第七题：习近平总书记指出，当今世界，人类正经历罕见的多重危机。面对层出不穷的全球性问题和挑战,我们应该坚持开放包容、协商合作，坚持和维护_____，积极推动构建人类命运共同体。",
        option: [
          {A: "单边主义"},
          {B: "保护主义"},
          {C: "多边主义"},
          {D: "自由主义"},
        ],
        anwser: "Qw==",
      },
      {
        title:
          "第八题：党的十九大报告指出，要坚持以人民为中心，必须坚持_____，坚持立党为公、执政为民，践行全心全意为人民服务的根本宗旨。",
        option: [
          {A: "人民主体地位"},
          {B: "国家主体地位"},
          {C: "党的主体地位"},
          {D: "公民主体地位"},
        ],
        anwser: "QQ==",
      },
      {
        title:
          "第九题：习近平总书记在庆祝中国共产党成立100周年大会上发表重要讲话并指出：江山就是人民、人民就是江山，打江山、守江山，守的是_____。",
        option: [
          {A: "人民的心"},
          {B: "发展成就"},
          {C: "制度体系"},
          {D: "人民民主专政"},
        ],
        anwser: "QQ==",
      },
      {
        title:
          "第十题：今天，我们比历史上任何时期都更接近、更有信心和能力实现______，同时必须准备付出更为艰巨、更为艰苦的努力。",
        option: [
          {A: "中华民族伟大复兴的目标"},
          {B: "脱贫攻坚战取得全面胜利的目标"},
          {C: "全面建成小康社会的目标"},
          {D: "世界第一强国的目标"},
        ],
        anwser: "QQ==",
      },
    ];

    const currentid = ref(0);
    const currentdata = reactive({
      data: {
        title: "题目",
      },
    });

    //利用list下标
    const select = ref("");
    const selected = (k) => {
      select.value = k;
      anwser[currentid.value] = k;
    };
    var anwser = [];
    const check = () => {
      for (var i = 0; i < anwser.length; i++) {
        if (anwser[i] == decodeURIComponent(atob(data[i].anwser))) {
          Fscore.value += 10;
        }
      }
    };

    const foward = () => {
      currentid.value -= 1;
      currentdata.data = data[currentid.value];
      anwser.pop();
      select.value = "";
    };
    const next = () => {
      currentid.value += 1;
      currentdata.data = data[currentid.value];
      select.value = "";
    };

    const Fscore = ref(0);
    //跳转结束页面
    let router = useRouter();

    const end = () => {
      check();
      router.push({
        //使用query的话，指定path或者name都行
        name: "end",
        params: {
          score: Fscore.value,
          name: sname,
          time: ele_timer.value
        },
      });
      clearInterval(timer);
    };

    //计时
    var n_sec = 0; //秒
    var n_min = 0; //分
    const ele_timer = ref("");
    //60秒 === 1分
    //60分 === 1小时
    const timer = setInterval(function () {
      var str_sec = n_sec;
      var str_min = n_min;
      if (n_sec < 10) {
        str_sec = "0" + n_sec;
      }
      if (n_min < 10) {
        str_min = "0" + n_min;
      }

      var time = str_min + "分" + str_sec + "秒";
      ele_timer.value = time;
      console.log(ele_timer.value)
      n_sec++;
      if (n_sec > 59) {
        n_sec = 0;
        n_min++;
      }
      if (n_min > 59) {
        n_sec = 0;
        n_hour++;
      }
    }, 1000);

    onMounted(() => {
      if (typeof sname == "undefined") {
        clearInterval(timer);
        router.push("/");
      }
      currentdata.data = data[0];
    });
    return {
      data,
      end,
      sname,
      foward,
      next,
      currentid,
      currentdata,
      select,
      selected,
    };
  },
};
</script>
