<template>
    <base-dialog v-if="inputIsValid" title="invalid input" @close="confirmError">
    <template #default>
        <p>Unfortunately at least one input value is valid. </p>
        <p>Please check all inputs...</p>
    </template>
    <template #actions>
        <base-button @click="confirmError">Okey</base-button>
    </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" ref="titleInput">
            </div>
            <!-- add refs to use them in methods -->
             <div class="form-control">
            <label for="description">Description</label>
           <textarea id="description" name="description" rows="3" ref="descInput"></textarea>
            </div>
            <div class="form-control">
            <label for="link">Title</label>
            <input id="link" name="link" type="url" ref="linkInput">
            </div>
            <div>
                <base-button type="submit">Add resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    data () {
        return {
            inputIsValid: false
        }
    },
    inject: ['addResource'],
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === ''){
                this.inputIsValid = true;
                return;
            }

            this.addResource(enteredTitle, enteredDescription, enteredLink); 
        },
        confirmError() {
            this.inputIsValid = false;
        }
    }
}
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