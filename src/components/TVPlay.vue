<template>
  <div class="tv-play">
    <i class="remove-tv" @click="handleRemove">X</i>
    <div>{{ tv.name }}</div>
    <div v-for="(actor, index) in tv.actors" :key="index">{{ actor }}</div>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import bus from "../utils/bus";
@Component
export default class TVPlay extends Vue {
  @Prop()
  tv: any;

  @Prop({ required: true })
  index?: number;

  handleRemove() {
    this.$emit("remove-tv", this.index);
  }

  mounted() {
    bus.$on("aaa", () => {
      console.log(this.tv.name + " " + this.tv.id);
    });
  }

  destroyed() {
    bus.$off("aaa")
  }
}
</script>
<style lang="scss" scoped>
.tv-play {
  position: relative;
  border: 1px lightblue solid;
  border-radius: 4px;
  padding: 15px;
  margin-bottom: 15px;
  .remove-tv {
    position: absolute;
    top: -10px;
    right: -10px;
    display: block;
    width: 20px;
    height: 20px;
    line-height: 20px;
    text-align: center;
    background: lightblue;
    color: #ffffff;
    font-size: 12px;
    border-radius: 50%;
  }
}
</style>
