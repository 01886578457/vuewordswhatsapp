<template>
    <div>
        <h2>{{what.name}}</h2>
        <p>{{what.remember ? '******': what.def}}</p>
        <div>
            <button @click="toggleWhat">{{what.remember?'Forgot':'Remembered'}}</button>
            <button @click="removeWhat">Remove</button>
        </div>
    </div>
</template>
<script>
export default {
  name: "WhatItem",
  props: ["what"],
  methods: {
    toggleWhat() {
      this.$emit("toggleWhat", this.what._id);
    },
    removeWhat() {
      this.$emit("removeWhat", this.what._id);
    }
  }
};
</script>
