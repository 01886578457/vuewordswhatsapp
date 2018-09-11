<template>
    <div>
        <div v-if="formVisibility">
        <input v-model="name" placeholder="name?"/>
        <br/>
        <input v-model="def" placeholder="Definition?"/>
        <div>
          <button @click="addWhat">Add</button>
          <button @click="toggleForm">Cancel</button>
        </div>          
      </div>
      <button v-else @click="toggleForm">+</button>
    </div>
</template>
<script>
export default {
  name: 'WhatForm',
  props: ['formVisibility'],
  data() {
    return {
      name: '',
      def: ''
    };
  },
  methods: {
    toggleForm() {
      this.$emit('toggleForm');
    },
    addWhat() {
      if (!this.name.trim() || !this.def.trim()) return;
      const payload = {
        name: this.name,
        def: this.def
      };
      this.$emit('addWhat', payload);
      this.name = '';
      this.def = '';
    }
  }
};
</script>
