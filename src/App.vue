<template>
  <div class="valign-wrapper" style="height: 100vh;">
    <div class="container">
      <div class="row">
        <div class="col s12 m8 offset-m2 l6 offset-l3">
          <div class="card z-depth-4">
            <div class="card-content">
              <span class="card-title blue-text-content" v-if="!edit.title"
               @click.prevent="edit.title = true">
                <div style="display: inline-flex; cursor: pointer;">
                  <i class="material-icons">edit</i>
                </div>
                {{ list.title }}
              </span>
              <span class="card-title blue-text-content" v-else>
                <div class="input-field">
                  <i class="material-icons prefix" @click.prevent="edit.title = false">save</i>
                  <input type="text" v-model="list.title">
                </div>
              </span>
              <ul class="collection">
                <li class="collection-item">
                  <a class="collection-item black-text" @click.prevent="addNewItem">
                    <i class="secondary-content material-icons black-text">add</i> Agregar</a>
                </li>
                <template v-for="(item, index) in items">
                  <todoitem :content="item" :key="`${index}_todoitem`"
                  v-on:deleteitem="deleteItem(index)"/>
                </template>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import todoitem from '@/components/todoitem.vue';

export default {
  name: 'App',
  components: {
    todoitem,
  },
  methods: {
    addNewItem() {
      this.items.push({ date: Date.now(), description: '' });
    },
    deleteItem(index) {
      this.$delete(this.items, index);
    },
  },
  data() {
    return {
      items: [],
      edit: {
        title: false,
      },
      list: {
        title: 'To Do List',
      },
    };
  },
};
</script>
<style>
.blue-text-content {
  color: #0068BD;
}
.card, .collection .collection-item {
  background-color: #F2A122;
}
/* label color */
.input-field label {
 color: #000;
}
/* label focus color */
.input-field input[type=text]:focus + label {
 color: #000;
}
/* label underline focus color */
.input-field input[type=text]:focus {
 border-bottom: 1px solid #000;
 box-shadow: 0 1px 0 0 #000;
}
/* valid color */
.input-field input[type=text].valid {
 border-bottom: 1px solid #000;
 box-shadow: 0 1px 0 0 #000;
}
/* invalid color */
.input-field input[type=text].invalid {
 border-bottom: 1px solid #000;
 box-shadow: 0 1px 0 0 #000;
}
/* icon prefix focus color */
.input-field .prefix.active {
 color: #000;
}

</style>
