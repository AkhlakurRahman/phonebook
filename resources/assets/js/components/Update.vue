<template>
    <div class="modal" :class="updateModal">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">Update {{ list.name }}'s Details</p>
            <button class="delete" aria-label="close" @click="closeModal"></button>
            </header>
            <section class="modal-card-body">
                <div class="field">
                    <label class="label">Name</label>
                    <div class="control">
                        <input class="input" type="text" placeholder="Enter name" v-model="list.name">
                    </div>
                </div>

                <div class="field">
                    <label class="label">Phone number</label>
                    <div class="control">
                        <input class="input" type="number" placeholder="Enter phone number" v-model="list.phone_number">
                    </div>
                </div>

                <div class="field">
                    <label class="label">Email</label>
                    <div class="control">
                        <input class="input" type="email" placeholder="Enter email" v-model="list.email">
                    </div>
                </div>
            </section>
            <footer class="modal-card-foot">
            <button class="button is-success" @click="update">Update</button>
            <button class="button" @click="closeModal">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['updateModal'],

        data() {
            return {
                list: {},
                errors: {}
            }
        },

        methods: {
            closeModal() {
                this.$emit('closeRequest');
            },

            update() {
                axios.patch(`/phonebook/${this.id}`, this.$data.list)
                    .then(response =>  this.closeModal())
                    .catch(error => this.errors = error.response.data.errors)
            }
        }
    }
</script>