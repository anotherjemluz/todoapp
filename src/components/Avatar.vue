<template lang="pug">
.avatar(:class="{ avatar__selected: !!selected }")
  .avatar_face
    img(src="../assets/profile.jpg")

  h2.avatar_name Olá, Jems.
  p.avatar_tips Meça duas vezes. Corte uma vez só. #[br] Você tem {{ todayTasks.length }} tarefas para hoje.
  p.avatar_date HOJE : {{ today | dateString }}
</template>

<script>
import { mapState, mapGetters } from "vuex";

export default {
  name: "Avatar",
  data() {
    return {
      today: new Date(),
    };
  },
  computed: {
    ...mapState(["selected"]),
    ...mapGetters(["todayTasks"]),
  },
  filters: {
    dateString(val) {
      return val
        .toDateString()
        .toUpperCase()
        .replace(/(\s\d{4})$/, ", $1");
    },
  },
};
</script>

<style lang="scss">
.avatar {
  display: flex;
  padding: 0 40px;
  height: 300px;
  justify-content: flex-end;
  flex-direction: column;
  transition: all 0.5s ease;
}
.avatar__selected {
  transform: translate3d(0, 20px, 0);
  opacity: 0;
}
.avatar_face {
  width: 44px;
  height: 44px;
  border-radius: 100%;
  border: 2px solid #fff;
  overflow: hidden;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);

  img {
    display: block;
    width: 100%;
    height: 100%;
  }
}
.avatar_name {
  margin-top: 32px;
  padding: 0 6px;
  font-size: 32px;
  letter-spacing: 1px;
  font-weight: 300;
}
.avatar_tips {
  margin-top: 16px;
  padding: 0 6px;
  font-size: 13px;
  font-weight: 100;
  opacity: 0.8;
  line-height: 1.6em;
}
.avatar_date {
  margin-top: 44px;
  margin-bottom: 16px;
  padding: 0 6px;
  font-size: 14px;
}
</style>