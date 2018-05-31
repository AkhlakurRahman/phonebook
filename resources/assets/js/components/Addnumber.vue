<template>
    <div class="modal" :class="openModal">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">Add Number</p>
            <button class="delete" aria-label="close" @click="closeModal"></button>
            </header>
            <section class="modal-card-body">
                <div class="field">
                    <label class="label">Name</label>
                    <div class="control">
                        <input class="input" :class="{'is-danger': errors.name}" type="text" placeholder="Enter name" v-model="input.name">
                    </div>
                    <small v-if="errors.name" class="has-text-danger">{{ errors.name[0] }}</small>
                </div>

                <div class="field">
                    <label class="label">Phone number</label>
                    <div class="control">
                        <input class="input" :class="{'is-danger': errors.phone_number}" type="number" placeholder="Enter phone number" v-model="input.phone_number">
                    </div>
                    <small v-if="errors.phone_number" class="has-text-danger">{{ errors.phone_number[0] }}</small>
                </div>

                <div class="field">
                    <label class="label">Email</label>
                    <div class="control">
                        <input class="input" :class="{'is-danger': errors.email}" type="email" placeholder="Enter email" v-model="input.email">
                    </div>
                    <small v-if="errors.email" class="has-text-danger">{{ errors.email[0] }}</small>
                </div>
            </section>
            <footer class="modal-card-foot">
            <button class="button is-success" @click="save">Add</button>
            <button class="button" @click="closeModal">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['openModal'],

        data() {
            return {
                input: {
                    name: '',
                    phone_number: '',
                    email: ''
                },
                errors: {}
            }
        },

        methods: {
            closeModal() {
                this.$emit('closeRequest');
            },

            save() {
                this.$emit('saveRequest');
            }
        }
    }
</script>