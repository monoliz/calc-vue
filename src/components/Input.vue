<template>
  <div class="form-group">
    <label class="pull-left">{{label}}</label>
    <input type="number" class="form-control" placeholder="Input 2 or more fields" @input="setNumFields" />
  </div>
</template>

<script>
  export default {
    data () {
      return {
        label: 'Fields number'
      }
    },
    methods: {
      setNumFields(e) {
        this.$emit('numFieldsChanged', e.target.value)
      }
    },
  }
    
</script>

<style>
</style>