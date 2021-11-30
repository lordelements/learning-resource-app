<template>
    <base-dialog v-if="inputIsInvalid" tittle="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
       <form @submit.prevent="submitData">
        <div class="form-control">
                <label for="tittle">Tittle</label>
                <input id="tittle" name="tittle" type="text" ref="tittleInput"/>
        </div>
        <div class="form-control">
                <label for="description">Discription</label>
               <textarea id="description" name="description" ref="descInput"></textarea>
        </div>
        <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="linkInput"/>
        </div>
        <div>
          <base-button type="submit">Add Resource</base-button>
        </div>
       </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data() {
        return {
            inputIsInvalid: false,
        };
    },
    methods: {
        submitData() {
            const enteredTittle = this.$refs.tittleInput.value;
            const enteredDiscription = this.$refs.descInput.value;
            const enteredUrl = this.$refs.linkInput.value;

            if (
                enteredTittle.trim() === '' || 
                enteredDiscription.trim() === '' || 
                enteredUrl.trim() === '') {
                    this.inputIsInvalid = true;
                    return;
            }

            this.addResource(enteredTittle, enteredDiscription, enteredUrl);
        },
        confirmError() {
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
        form {
        margin: 1rem;
        border: 1px solid #ccc;
        border-radius: 12px;
        padding: 1rem;
        }

        .form-control {
        margin: 0.5rem 0;
        }

        label {
        font-weight: bold;
        margin-bottom: 0.5rem;
        display: block;
        }

        input,
        textarea {
        display: block;
        width: 100%;
        font: inherit;
        border: 1px solid #ccc;
        padding: 0.15rem;
        resize: none;
        }

        input:focus,
        textarea:focus {
        border-color: #3d008d;
        background-color: #faf6ff;
        outline: none;
        }

        .errors {
        font-weight: bold;
        color: red;
        }

        .actions {
        text-align: center;
        }
</style>