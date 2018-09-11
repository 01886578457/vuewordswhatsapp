<template>
    <div>
      <what-form 
        :formVisibility="formVisibility" 
        @toggleForm="toggleForm" 
        @addWhat="addWhat"
      >
      </what-form>
      <what-filter 
        :filter="filter" 
        @filterChanged="handleFilterChanged"
      >
      </what-filter>
      <what-item 
        v-for="what in filteredWhats" 
        :key="what._id" 
        :what="what"
        @toggleWhat="toggleWhat"
        @removeWhat="removeWhat"
      >
      </what-item>
    </div>
</template>

<script>
import WhatItem from './WhatItem';
import WhatFilter from './WhatFilter';
import WhatForm from './WhatForm';
export default {
  name: 'WhatsApp',
  components: {
    WhatItem,
    WhatFilter,
    WhatForm
  },
  data() {
    return {
      filter: 'SHOW_ALL',
      formVisibility: false,
      name: '',
      def: '',
      whats: [
        { _id: 1, name: 'Vue', def: 'javascript framework', remember: true },
        { _id: 2, name: 'Vuex', def: 'framework', remember: true },
        {
          _id: 3,
          name: 'Angular',
          def: 'google javascript framework',
          remember: false
        },
        { _id: 4, name: 'Reactjs', def: 'facebook javascript framework', remember: true }
      ]
    };
  },
  methods: {
    toggleWhat(_id) {
      const what = this.whats.find(w => w._id === _id);
      what.remember = !what.remember;
    },
    toggleForm() {
      this.formVisibility = !this.formVisibility;
    },
    removeWhat(_id) {
      const index = this.whats.findIndex(w => w._id === _id);
      this.whats.splice(index, 1);
    },
    handleFilterChanged(filter) {
      this.filter = filter;
    },
    addWhat(payload) {
      const what = {
        _id: Date.now(),
        name: payload.name,
        def: payload.def,
        remember: false
      };
      this.whats.unshift(what);
    },
    
  },
  computed: {
    filteredWhats() {
      if (this.filter === 'SHOW_FORGOT')
        return this.whats.filter(w => !w.remember);
      if (this.filter === 'SHOW_REMEMBERED')
        return this.whats.filter(w => w.remember);
      return this.whats;
    }
  }
};
</script>

