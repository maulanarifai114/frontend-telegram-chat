<template>
  <div>
    <label :for="id" class=" align-self-start">{{label}}</label>
    <input :type="type" :id="id" v-model="data" maxlength="64" :placeholder="placeholder" :value="value" @input="inputData" required>
  </div>
</template>

<script>
export default {
  name: 'InputText',
  props: ['id', 'type', 'placeholder', 'label', 'value'],
  data () {
    return {
      data: ''
    }
  },
  methods: {
    inputData (e) {
      this.$emit('input', this.data)
    }
  }
}
</script>

<style lang="scss" scoped>

label {
  font-family: Rubik;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  color: #848484;
  opacity: 0.75;
}

input {
  font-family: Rubik;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 19px;
  color: #232323;
  border-bottom: 1px solid #adadad;
  padding: 15px 0;
  width: 100%;
}

input::placeholder {
  color: rgba(35, 35, 35, 0.2);
}

</style>
