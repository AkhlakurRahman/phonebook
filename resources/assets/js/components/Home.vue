<template>
	<div>
		<nav class="panel column is-8 is-offset-2">
			<p class="panel-heading">
				Phonebook
			</p>

			<div class="panel-block">
				<button class="button is-link is-outlined is-fullwidth" @click="addNumber">
					Add Number
				</button>
			</div>
			<div class="panel-block">
				<p class="control has-icons-left">
				<input class="input is-small" type="text" placeholder="search">
				<span class="icon is-small is-left">
					<i class="fa fa-search" aria-hidden="true"></i>
				</span>
				</p>
			</div>
			<a class="panel-block" v-for="item,key in lists">
				<span class="column is-9">
					{{ item.name }}
				</span>
					<span class="panel-icon column is-1">
						<i class="has-text-danger fa fa-trash" aria-hidden="true" @click="deleteEntry(key, item.id)"></i>
					</span>
					<span class="panel-icon column is-1">
						<i class="has-text-info fa fa-edit" aria-hidden="true" @click="updateDetails(key)"></i>
					</span>
					<span class="panel-icon column is-1">
						<i class="has-text-primary fa fa-eye" aria-hidden="true" @click="showDetails(key)"></i>
					</span>
			</a>
		</nav>

		<Addnumber :openModal="addClass" @closeRequest="closeModal" @saveRequest="save"></Addnumber>
		<showdetails :showModal="showDetailsClass" @closeRequest="closeModal"></showdetails>
		<Updatedetails :updateModal="updateDetailsClass" @closeRequest="closeModal"></Updatedetails>
	</div>
</template>

<script>
	let Addnumber = require('./Addnumber.vue');
	let Showdetails = require('./Showdetails.vue');
	let Updatedetails = require('./Update.vue');

	export default {
		components: {
			Addnumber,
			Showdetails,
			Updatedetails,
		},
		
		data() {
			return {
				addClass: '',
				showDetailsClass: '',
				updateDetailsClass: '',
				lists: '',
				errors: '',
			}
		},

		mounted() {
			axios.post('/getData')
				.then(response => this.lists = response.data)
				.catch(error => this.errors = error.response.data.errors)
		},

		methods: {
			addNumber() {
				this.addClass = 'is-active';
			},

			closeModal() {
				this.addClass = this.showDetailsClass = this.updateDetailsClass ='';
			},

			showDetails(key) {
				this.$children[1].list = this.lists[key];
				this.showDetailsClass = 'is-active';
			},

			updateDetails(key) {
				this.$children[2].list = this.lists[key];
				this.updateDetailsClass = 'is-active';
			},

			deleteEntry(key, id) {
				if (confirm('Are you sure?')) {
					axios.delete(`/phonebook/${id}`)
						.then(response => this.lists.splice(key, 1))
						.catch(error => this.errors = error.response.data.errors)
					}

			},

			save() {
                axios.post('/phonebook', this.$data.input)
                    .then(response =>  {
                        this.closeModal()
                        this.$parent.lists.push(response.data)
                        this.$parent.lists.sort(function(a, b) {
                            if (a.name > b.name) {
                                return 1;
                            } else if (a.name < b.name) {
                                return -1;
                            }
                        })
                        this.input = ''
                    })
                    .catch(error => this.errors = error.response.data.errors)
            }
		}
	}
</script>
