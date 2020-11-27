<template>
  <div class="home">
    <tv-play
      v-for="(tv, index) in tvList"
      :key="tv.id"
      :tv="tv"
      :index="index"
      @remove-tv="removeTv"
    ></tv-play>
    名字：<input type="text" v-model="newTv.name" />
    <button @click="addTv">添加</button>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import TvPlay from "../components/TVPlay.vue";
import bus from "../utils/bus";
interface Tv {
  id: number;
  name: string;
  actors: string[];
}
@Component({
  components: {
    TvPlay
  }
})
export default class Home extends Vue {
  private uid = 0;

  tvList: Tv[] = [
    {
      id: this.uid++,
      name: "美人为馅",
      actors: ["白宇", "杨蓉"]
    },
    {
      id: this.uid++,
      name: "沉默的真相",
      actors: ["白宇", "廖凡"]
    },
    {
      id: this.uid++,
      name: "银河补习班",
      actors: ["白宇", "邓超"]
    }
  ];

  newTv: Tv = {
    id: this.uid++,
    name: "",
    actors: []
  };

  removeTv(index: number) {
    this.tvList.splice(index, 1);
    bus.$emit("aaa");
  }

  addTv() {
    this.tvList.push(this.newTv);
    this.newTv = {
      id: this.uid++,
      name: "",
      actors: []
    };
  }
}
</script>
<style lang="scss" scoped>
.home {
  margin: 30px auto;
  width: 70%;
}
</style>
