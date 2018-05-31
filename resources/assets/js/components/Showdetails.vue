<template>
    <div class="modal" :class="showModal">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">{{ list.name }}'s detail</p>
            <button class="delete" aria-label="close" @click="closeModal"></button>
            </header>
            <section class="modal-card-body">
                <li class="panel-block">
                    <label class="column is-2"><b>Name:</b></label> {{ list.name }}
                </li>

                <li class="panel-block">
                    <label class="column is-2"><b>Phone:</b></label> {{ list.phone_number }}
                </li>

                <li class="panel-block">
                    <label class="column is-2"><b>Email:</b></label> {{ list.email }}
                </li>
            </section>
            <footer class="modal-card-foot">
            <button class="button" @click="closeModal">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['showModal'],

        methods: {
            closeModal() {
                this.$emit('closeRequest');
            },
        },

        data() {
			return {
				list: '',
			}
		},
    }
</script>