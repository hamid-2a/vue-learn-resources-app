<template>
  <BaseCard>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" type="text" name="title" ref="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="description"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="link" />
      </div>
      <div>
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>

  <teleport to="body">
    <error-input v-if="isInputIncorrect">
      <template #header>
        <h2>Invalid input &#128580;</h2>
      </template>

      <p><b>Unfortunately, at least one input value is invalid.</b></p>
      <p>Please make sure you fill all fields correctly!</p>

      <template #actions>
        <base-button @click="closeErrorInput">Got it</base-button>
      </template>
    </error-input>
  </teleport>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import ErrorInput from '../UI/ErrorInput.vue';

export default {
  components: { ErrorInput, BaseButton },
  props: ['ErrorInput'],

  inject: ['addResource'],

  data() {
    return {
      isInputIncorrect: false,
    };
  },

  methods: {
    submitResource() {
      const titleInput = this.$refs.title.value;
      const descInput = this.$refs.description.value;
      const linkInput = this.$refs.link.value;

      if (
        titleInput.trim() === '' ||
        descInput.trim() === '' ||
        linkInput.trim() === ''
      ) {
        this.isInputIncorrect = true;
        return;
      }

      this.addResource(titleInput, descInput, linkInput);

      this.$refs.title.value = '';
      this.$refs.description.value = '';
      this.$refs.link.value = '';
    },

    closeErrorInput() {
      this.isInputIncorrect = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>