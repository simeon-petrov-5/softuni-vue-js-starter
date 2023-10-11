<script>
const focus = {
  mounted: (el, binding, vnode) => {
    console.log(el, binding, vnode);
    el.focus();
  },
};

export default {
  directives: {
    focus,
  },
  beforeRouteEnter(to, from) {
    console.log('beforeRouteUpdate', to, from);
    return true;
  },
  props: {
    msg: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      link: {
        url: 'user/edit',
        label: 'Edit your profile',
        rou: this.$route,
      },
    };
  },
  watch: {
    '$route.params': function (to, from) {
      console.log(to, from);
    },
  },
  methods: {
    updateName() {
      this.fullName = 'John Kennedy';
    },
    onRouter() {
      this.$router.push('haha');
    },
  },
};
</script>

<template>
  <h1>{{ $route.fullPath }}</h1>
  <router-link :to="link.url">
    {{ link.label }}
  </router-link>
  <button @click="onRouter">
    BTN router test
  </button>
  <input
    id=""
    v-focus:[directiveArg].some.thing="'noice'"
    type="text"
    name=""
    placeholder="ha"
  >
</template>
