<script>
import Button from '../reusable/Button.vue';
import emailjs from 'emailjs-com';
export default {
	components: { Button },
	data() {
		return {
			formData: {
				name: '',
				subject: '',
				message: '',
			},
			formSubmitted: false,
			formError: false,
			isDialogOpen: false,
		};
	},
	methods: {
		async submitForm() {
			try {
				const serviceID = 'service_svwpz2f';
				const templateID = 'template_hvs4tvd';
				const userID = 'A4tKO5FBi7rHfoE7Z';
				const name = 'Octavia Lintang';

				const templateParams = {
					to_name: name,
					subject: this.formData.subject,
					from_name: this.formData.name,
					message: this.formData.message,
				};

				const response = await emailjs.send(
					serviceID,
					templateID,
					templateParams,
					userID
				);
				console.log(templateParams);
				if (response.status === 200) {
					this.formSubmitted = true;
					this.isDialogOpen = true;
					this.clearForm();
				} else {
					this.formError = true;
				}
			} catch (error) {
				this.formError = true;
				console.error('Error sending email:', error);
			}
		},
		clearForm() {
			this.formData.name = '';
			this.formData.subject = '';
			this.formData.message = '';
		},
		closeDialog() {
			this.isDialogOpen = false; // Close the dialog
		},
	},
};
</script>

<template>
	<div class="w-full md:w-1/2">
		<div
			class="leading-loose max-w-xl m-4 p-7 bg-secondary-light dark:bg-secondary-dark rounded-xl shadow-xl text-left">
			<p class="font-general-medium text-primary-dark dark:text-primary-light text-2xl mb-8">
				Contact Form
			</p>
			<form @submit.prevent="submitForm" class="font-general-regular space-y-7">
				<div>
					<label for="name-input" class="block mb-2 text-lg text-primary-dark dark:text-primary-light">Full
						Name:</label>
					<input type="text" id="name-input" v-model="formData.name"
						class="w-full px-5 py-3 border border-gray-300 dark:border-primary-dark border-opacity-50 text-primary-dark dark:text-secondary-light bg-ternary-light dark:bg-ternary-dark rounded-md shadow-sm text-md">
				</div>
				<div>
					<label for="subject-input"
						class="block mb-2 text-lg text-primary-dark dark:text-primary-light">Subject:</label>
					<input type="text" id="subject-input" v-model="formData.subject"
						class="w-full px-5 py-3 border border-gray-300 dark:border-primary-dark border-opacity-50 text-primary-dark dark:text-secondary-light bg-ternary-light dark:bg-ternary-dark rounded-md shadow-sm text-md">
				</div>
				<div>
					<label for="message-input"
						class="block mb-2 text-lg text-primary-dark dark:text-primary-light">Message:</label>
					<textarea id="message-input" v-model="formData.message"
						class="w-full px-5 py-2 border border-gray-300 dark:border-primary-dark border-opacity-50 text-primary-dark dark:text-secondary-light bg-ternary-light dark:bg-ternary-dark rounded-md shadow-sm text-md"></textarea>
				</div>
				<div>
					<Button title="Send Message"
						class="px-4 py-2.5 text-white tracking-wider bg-indigo-500 hover:bg-indigo-600 focus:ring-1 focus:ring-indigo-900 rounded-lg duration-500"
						type="submit" aria-label="Send Message" />
				</div>
			</form>
		</div>

		<div v-if="isDialogOpen" class="fixed inset-0 flex items-center justify-center z-50">
			<div class="bg-white dark:bg-secondary-dark p-6 rounded-lg shadow-lg">
				<p class="font-general-medium text-primary-dark dark:text-primary-light text-2xl mb-4">
					Message Sent Successfully!
				</p>
				<p class="font-general-regular text-primary-dark dark:text-primary-light text-lg">
					Thank you for contacting us. Your message has been sent successfully.
				</p>
				<button @click="closeDialog"
					class="mt-6 px-4 py-2 text-white tracking-wider bg-indigo-500 hover:bg-indigo-600 focus:ring-1 focus:ring-indigo-900 rounded-lg duration-500">
					Close
				</button>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>