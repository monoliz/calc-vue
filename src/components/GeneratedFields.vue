<template>
  <div>
  <input type="number" @input="inputChange" class="form-control" />
    <div class="btn-group" v-if="id+1 !== numFields" >
      <button type="button" class="btn btn-default">{{operationText}}</button>
      <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        <span class="caret"></span>
        <span class="sr-only">Toggle Dropdown</span></button>
      <ul class="dropdown-menu">
        <li><a name="+" @click="operationChange">+</a></li>
        <li><a name="-" @click="operationChange">-</a></li>
        <li><a name="*" @click="operationChange">*</a></li>
        <li><a name="/" @click="operationChange">/</a></li>
      </ul>
    </div>
  </div> 
</template>

<script>
  export default {
    data () {
      return {
        operationText: 'Choose an operation',
      }
    },
    props: ['id', 'numFields'],
    methods: {
      operationChange (e) {
        this.operationText = e.target.name
        let op = e.target.name
        this.$emit ('operationChanged', [this.id, op])
      },
      inputChange (e) {
        let inp = e.target.value
        this.$emit ('inputChanged', [this.id, inp])
      }
    } 
  }
  
</script>