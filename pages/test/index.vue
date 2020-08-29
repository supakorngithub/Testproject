/* eslint-disable no-console */
<template>
  <div>
    <a-card title="TEST">
      <a-row>
        <a-col :span="6">Title</a-col>
        <a-col :span="3">Hour</a-col>
        <a-col :span="3">Min</a-col>
        <a-col :span="12"></a-col>
      </a-row>
      <a-row>
        <a-col :span="6">
          <a-input ref="focus" v-model="title" class="w-90" />
        </a-col>

        <a-col :span="3">
          <a-input-number v-model="hour" :min="0" :max="23" class="w-90" />
        </a-col>
        <a-col :span="3">
          <a-input-number v-model="min" :min="0" :max="59" class="w-90" />
        </a-col>
        <a-col :span="6"></a-col>
        <a-col :span="6">
          <a-button type="primary" class="btn-add" @click="onAdd">add</a-button>
        </a-col>
      </a-row>
      <br />
      <hr />
      <br />
      <a-row>
        <div v-if="items.length > 0">
          <a-col :span="12">Title</a-col>
          <a-col :span="3">Hour/Min</a-col>
        </div>
      </a-row>
      <div v-for="(item, index) in items" :key="index">
        <a-row>
          <a-col :span="12">{{ item.title }} </a-col>
          <a-col :span="6">{{ item.hour }} : {{ item.min }}</a-col>
          <a-col :span="3">
            <a-button type="primary" @click="onEdit(index)">edit</a-button>
          </a-col>
          <a-col :span="3">
            <a-button type="danger" @click="onDel(index)">delete</a-button>
          </a-col>
        </a-row>
      </div>
    </a-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: undefined,
      hour: undefined,
      min: undefined,
      items: [
        // { title: '1.test', hour: '1', min: '1' },
        // { title: '2.test', hour: '2', min: '2' },
        // { title: '3.test', hour: '3', min: '3' },
      ],
      indexs: undefined,
    }
  },
  mounted() {
    this.$refs.focus.focus()
  },
  methods: {
    onAdd() {
      // console.log(this.indexs)
      // eslint-disable-next-line no-console
      // if (this.indexs) {
      if (this.indexs !== undefined) {
        // const itemedit = this.items
        this.items[this.indexs].title = this.title
        this.items[this.indexs].hour = this.hour
        this.items[this.indexs].min = this.min

        // this.items.splice(this.indexs, 1)
      } else if (
        this.title !== undefined &&
        this.hour !== undefined &&
        this.min !== undefined
      ) {
        this.items.push({
          title: this.title,
          hour: this.hour,
          min: this.min,
        })
      } else {
        // eslint-disable-next-line no-console
        alert('Incomplete data')
      }

      this.title = undefined
      this.hour = undefined
      this.min = undefined
      this.indexs = undefined
    },
    onEdit(index) {
      // console.log(index)
      const itemedit = this.items

      this.title = itemedit[index].title
      this.hour = itemedit[index].hour
      this.min = itemedit[index].min
      this.indexs = index
    },
    onDel(index) {
      this.items.splice(index, 1)
    },
  },
}
</script>

<style scoped>
.w-90 {
  width: 90%;
}
.btn-add {
  background-color: #3b8070;
  border: 1px solid #3b8070;
}
</style>
