<template>
  <li class="collection-item avatar">
    <h5 class="blue-text-content" v-if="!edit.title" @click.prevent="edit.title = true">
      <div style="display: inline-flex; cursor: pointer;">
        <i class="material-icons">edit</i>
      </div>
      {{content.description}}</h5>
    <span v-else>
      <div class="input-field">
        <i class="material-icons prefix" @click.prevent="edit.title = false"
        v-show="content.description.length">save</i>
        <input type="text" v-model="content.description"
        placeholder="Agrega una descripción">
      </div>
    </span>
    <p> {{content.date | humanize}}
    </p>
      <a class="secondary-content" v-if="!edit.title" @click.prevent="$emit('deleteitem')">
        <i class="material-icons blue-text-content">delete</i>
      </a>
  </li>
</template>

<script>
export default {
  name: 'todoitem',
  props: {
    content: {
      type: Object,
      default: () => ({}),
    },
  },
  filters: {
    humanize(date) {
      const parsedDate = new Date(date);
      return parsedDate.toLocaleString();
    },
  },
  mounted() {
    this.edit.title = !this.content.description.length;
  },
  data() {
    return {
      edit: {
        title: false,
      },
    };
  },
};
</script>
