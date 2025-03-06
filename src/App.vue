<template>
  <div>
    <parent/>
  </div>
</template>

<script>
import Parent from './components/Parent.vue';
export default {
  components: { Parent },
  data () {
    return {
      name: []
    };
  },
  methods: {
    name () {
      //
    }
  }
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
}
</style>