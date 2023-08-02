<script>
export default {
	setup() {
		return {
			bios: [
				{
					id: 1,
					bio:
						'Hello, my name is Octavia Lintang Pramesti. Im a student at the Faculty of Computer Science, Brawijaya University. I have experience in website development, mobile app development, and UI/UX design. I am passionate about activities that require problem-solving skills and have an interest in the software engineering profession.',
				}
			],
		};
	},
};
</script>

<template>
	<div class="block sm:flex sm:gap-10 mt-10 sm:mt-20">
		<!-- About profile image -->
		<div class="w-full sm:w-1/4 mb-7 sm:mb-0">
			<img
				src="@/assets/images/profile.jpeg"
				class="rounded-xl w-96"
				alt=""
			/>
		</div>

		<!-- About details -->
		<div class="w-full sm:w-3/4 text-left">
			<p
				v-for="bio in bios"
				:key="bio.id"
				class="font-general-regular mb-4 text-ternary-dark dark:text-ternary-light text-lg"
			>
				{{ bio.bio }}
			</p>
		</div>
	</div>
</template>
