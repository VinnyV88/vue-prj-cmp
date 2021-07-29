<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
  <template #default>
  <p>Unfortunately, at least one input is invalid!</p>
  <p>Please check all input fields to ensure something was entered for all of them.</p>
  </template>
  <template #actions>
    <base-button @click="confirmError">Okay</base-button>
  </template>
  </base-dialog>
  <base-card>
    <template v-slot:header>
      <h2>Add Resource</h2>
    </template>
    <template v-slot:default>
      <form @submit.prevent="submitData">
        <div class="form-control">
          <label for="inTitle">Title</label>
          <input id="inTitle" name="inTitle" type="text" ref="inTitle" />
        </div>
        <div class="form-control">
          <label for="inDesc">Description</label>
          <textarea
            id="inDesc"
            name="inDesc"
            rows="3"
            type="text"
            ref="inDesc"
          ></textarea>
        </div>
        <div class="form-control">
          <label for="inLink">Link</label>
          <input id="inLink" name="inLink" type="url" ref="inLink" />
        </div>
        <div class="form-control">
          <base-button type="submit">Add Resource</base-button>
        </div>
      </form>
    </template>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    submitData() {
      const title = this.$refs.inTitle.value.trim();
      const desc = this.$refs.inDesc.value.trim();
      const link = this.$refs.inLink.value.trim();

      if (title === '' || desc === '' || link === '') {
        this.inputIsInvalid = true;
      } else {
        this.addResource(title, desc, link);
      }
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
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
