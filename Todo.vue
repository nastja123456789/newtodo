<template>
  <li>
    <button
        v-if="!isEditing"
        :class="{ completed }"
        @click="$emit('on-toggle')"
    >
      <span>{{description}}</span>
    </button>
    <form v-else @submit.present="finishEditing()">
      <input
      type="text"
      v-model="newTodoDescription"
      @blur="finishEditing()"
      ref="newTodo"
      />
    </form>
    <button
        @click="startEditing()"
    />
  <button @click="$emit('on-delete')">
    <span></span>
  </button>
  </li>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      newTodoDescription: ""
    };
  },
  props: {
    description: String,
    completed: Boolean
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.Editing = true;
        this.$nextTick(() => this,$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    }
  }
};
</script>

<style lang="scss" scoped>

</style>