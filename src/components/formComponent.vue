<template>
  <form @submit.prevent="handleSubmit">
    <slot :values="values" :errors="errors" :isSubmitting="isSubmitting" :handleSubmit="handleSubmit"/>
  </form>
</template>

<script>
import { reactive } from "vue";

export default {
  props: {
    initialValues: {
      type: Object,
      required: true
    },
    validate: {
      type: Function,
      default: () => {}
    },
    onSubmit: {
      type: Function,
      required: true
    }
  },
  setup(props) {
    const state = reactive({
      values: props.initialValues,
      errors: {},
      isSubmitting: false
    });

    const handleSubmit = async () => {
      state.isSubmitting = true;
      try {
        await props.validate(state.values);
        await props.onSubmit(state.values);
      } catch (errors) {
        state.errors = errors;
      } finally {
        state.isSubmitting = false;
      }
    };

    return { ...state, handleSubmit };
  }
};
</script>
