<template>
  <div class="record-nav">
    <div class="right"></div>
    <div class="type">
      <ul>
        <li :class="{selected:type==='-'}" @click="changeType('-')">支出</li>
        <li :class="{selected:type==='+'}" @click="changeType('+')">收入</li>
      </ul>
    </div>
    <div class="cancel" @click="changeAddToggle">取消</div>
  </div>
</template>

<script>
import Vue from 'vue'
import {Component} from 'vue-property-decorator'
@Component
export default class RecordNav extends Vue{
  get type(){
      return this.$store.state.auth.addDate.type
  }
  changeAddToggle() {
    this.$store.commit("changeAddToggle");
    this.$store.commit("changeCurrentKind", {
      iconName: undefined,
      textName: undefined
      });
      setTimeout(() => {
        this.$router.push("/detail");
      }, 400);
  }
  changeType(type) {
    this.$store.commit("changeType", type);
  }
}

</script>




<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";
.record-nav {
  background: $color-yellow;
  width: 100vw;
  padding: 0 10px;
  display: flex;
  .right {
    width: 80px;
  }
  .cancel {
    width: 80px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .type {
    flex-grow: 1;
    font-weight: 700;
    ul {
      display: flex;
      li {
        flex-grow: 1;
        text-align: center;
        position: relative;
        padding: 10px 0;
        &.selected {
          &::after {
            content: "";
            position: absolute;
            bottom: 0;
            left: 10%;
            height: 3px;
            width: 80%;
            background: black;
          }
        }
      }
    }
  }
}
</style>