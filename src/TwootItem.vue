<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <div class="twoot-item_user">@{{ username }}</div>
    <div class="twoot-item_content">
      {{ twoot.content }}
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favouriteTwoot(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style lang="scss" scoped>
.twoot-item {
  padding: 20px;
  background: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  width: 90%;
  
  .twoot-item:hover {
    transform: scale(1.1, 1.1);
  }
  .twoot-item_user {
    font-weight: bold;
  }
}
</style>
