<template>
    <div>
        <select :value="filter" @change="onFilterChanged">
            <option value="SHOW_ALL">SHOW ALL</option>
            <option value="SHOW_FORGOT">SHOW FORGOT</option>
            <option value="SHOW_REMEMBERED">SHOW REMEMBERED</option>
        </select>
    </div>
</template>
<script>
export default {
  name: 'WhatFilter',
  props: ['filter'],
  methods: {
    onFilterChanged(e) {
      this.$emit('filterChanged', e.target.value);
    }
  }
};
</script>
