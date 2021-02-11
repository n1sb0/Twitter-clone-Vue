<template>
  <div class="twit-item" @click="favouriteTwit(twit.id)">
    <div class="user-profile__twit">
      <div class="twit-item__user">@{{ username }}</div>
      <div class="twit-item__contnt">
        {{ twit.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwitItem",

  props: {
    username: {
      type: String,
      required: true,
    },
    twit: {
      type: Object,
      required: true,
    },
  },

  methods: {
    favouriteTwit(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style lang="scss" scoped>
.twit-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #e5e5e5;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin-top: 5px;

  &:hover {
    transform: scale(1.1, 1.1);
  }

  .twit-item__user {
    padding: auto;
    font-weight: bold;
  }

  .twit-item__contnt {
    margin-top: 10px;
  }
}
</style>