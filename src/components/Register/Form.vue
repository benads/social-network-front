<template>
	<div class="hello">
		<h1>Je suis le component LOGIN</h1>
		<b-form @submit="onSubmit" @reset="onReset" v-if="show">
			<b-form-group
				id="input-group-1"
				label="Email address:"
				label-for="input-1"
			>
				<b-form-input
					id="input-1"
					v-model="form.email"
					type="email"
					required
					placeholder="Enter email"
				></b-form-input>
			</b-form-group>

			<b-form-group id="input-group-2" label="Mot de passe" label-for="input-2">
				<b-form-input
					id="input-2"
					v-model="form.password"
					required
					placeholder="Enter password"
				></b-form-input>
			</b-form-group>

			<b-form-group id="input-group-2" label="Pseudo" label-for="input-2">
				<b-form-input
					id="input-2"
					v-model="form.pseudo"
					required
					placeholder="Entrer pseudo"
				></b-form-input>
			</b-form-group>

			<b-form-group id="input-group-2" label="Nom" label-for="input-2">
				<b-form-input
					id="input-2"
					v-model="form.name"
					required
					placeholder="Entrer nom"
				></b-form-input>
			</b-form-group>

			<b-form-group id="input-group-2" label="Nom de famille" label-for="input-2">
				<b-form-input
					id="input-2"
					v-model="form.last_name"
					required
					placeholder="Entrer nom de famille"
				></b-form-input>
			</b-form-group>

			<b-form-group id="input-group-2" label="Mot de passe" label-for="input-2">
				<b-form-input
					id="input-2"
					v-model="form.first_name"
					required
					placeholder="Enter prénom"
				></b-form-input>
			</b-form-group>

			<b-button type="submit" variant="primary">Submit</b-button>
			<b-button type="reset" variant="danger">Reset</b-button>
		</b-form>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "Login",
	props: {
		msg: String,
	},
	data() {
		return {
			form: {
				email: "",
                password: "",
                pseudo: "",
                first_name: "",
                last_name: "",
                name: ""
			},
			show: true,
		};
	},
	methods: {
		onSubmit(evt) {
			evt.preventDefault();
			axios
				.post("http://localhost:81/api/register", JSON.stringify(this.form), {
					headers: { "Content-Type": "application/json" },
				})
				.then(function(response) {
					localStorage.setItem("token", response.data.access_token);
				})
				.catch(function(error) {
					console.log(error);
				});
		},
		onReset(evt) {
			evt.preventDefault();
			// Reset our form values
			this.form.email = "";
            this.form.password = "";
            this.form.pseudo = "";
            this.form.first_name = "";
            this.form.last_name = "";
            this.form.name = "";
			// Trick to reset/clear native browser form validation state
			this.show = false;
			this.$nextTick(() => {
				this.show = true;
			});
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}
</style>
