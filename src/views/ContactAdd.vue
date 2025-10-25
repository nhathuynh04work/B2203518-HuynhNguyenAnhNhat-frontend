<template>
	<div class="page">
		<h4>Thêm Liên hệ</h4>
		<ContactForm :contact="newContact" @submit:contact="addContact" />
		<p>{{ message }}</p>
	</div>
</template>

<script>
import ContactForm from "../components/ContactForm.vue";
import ContactService from "../services/contact.service";

export default {
	components: {
		ContactForm,
	},
	data() {
		return {
			// A new, empty contact object for the form
			newContact: {
				name: "",
				email: "",
				address: "",
				phone: "",
				favorite: false,
			},
			message: "",
		};
	},
	methods: {
		async addContact(data) {
			try {
				await ContactService.create(data);
				// Use the message data property instead of alert()
				this.message = "Liên hệ được thêm thành công.";

				// Optional: Navigate back to the main page after a short delay
				setTimeout(() => {
					this.$router.push({ name: "contactbook" });
				}, 1000); // 1-second delay
			} catch (error) {
				console.log(error);
				this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
			}
		},
	},
	created() {
		this.message = "";
	},
};
</script>
