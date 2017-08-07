<template>
  <div class="todo">
    {{message}}
    <!--
    something warning message with using `v-model`
    <input type="text" v-model="inputText" @input="onChangeText"/>
    -->
    <v-text-field
      name="input-1"
      label="Add To do list here..."
      :value="inputText" @change="onChangeText"
    ></v-text-field>
    <v-btn light @click="onAdd">Add</v-btn>
    <v-btn light @click="onTest">Test append button</v-btn>

    <v-container fluid>
      <v-layout row wrap>
        <v-flex xs6>
          <v-list v-for="item in list">
            {{ item.title }}
          </v-list>
        </v-flex>
        <v-flex xs6>
          <v-list v-for="item in list">
            <button @click="onDel(item)"><v-icon>fa-trash</v-icon></button>
          </v-list>
        </v-flex>
      </v-layout>
    </v-container>


  </div>
</template>

<script>
console.log('on todo view vue')
export default {
  name: 'todo-list',
  data () {
    return {
      message: 'Hello Vue!'
    }
  },
  computed: {
    list () {
      return this.$store.getters.activeList
    },
    inputText () {
      return this.$store.getters.getInputText
    }
  },
  methods: {
    onAdd (event) {
      console.log('on add')
      // this.$store.commit('addItem')
      this.$store.dispatch('addItem')
    },
    onChangeText (event) {
      console.log('on change text')
      if (event && event.target) {
        console.log(event.target.value)
        this.$store.commit('changeText', event.target.value)
      }
    },
    onTest () {
      console.log('on test')
      this.$store.dispatch('appendText')
    },
    onDel (item) {
      console.log('on del', item)
      this.$store.dispatch('delItem', item)
    }
  }
}
</script>
