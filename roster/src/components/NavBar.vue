<template>
	<div class="h-12 bg-white border-b px-12 flex items-center">
		<div class="flex items-center space-x-1">
			<a href="/desk" class="text-black-600 hover:text-black-700 flex items-center">
				<DeskMonitorLogo class="h-4 w-4" />
			</a>
			<span class="mx-2 text-gray-400">/</span>
			<a href="/desk/shift-&-attendance" class="text-gray-600 hover:text-gray-700 flex items-center">
				Shift & Attendance
			</a>
			<span class="mx-2 text-gray-400">/</span>
			<span class="font-medium">Roster</span>
		</div>
		<Dropdown
			class="ml-auto"
			:options="[
				{
					label: 'My Account',
					onClick: () => goTo('/me'),
				},
				{
					label: 'Log Out',
					onClick: () => logout.submit(),
				},
				{
					label: 'Switch to Desk',
					onClick: () => goTo('/app'),
				},
			]"
		>
			<Avatar
				:label="props.user?.full_name"
				:image="props.user?.user_image"
				size="lg"
				class="cursor-pointer"
			/>
		</Dropdown>
	</div>
</template>

<script setup lang="ts">
import { FeatherIcon, Dropdown, Avatar, createResource } from "frappe-ui";
import DeskMonitorLogo from "../icons/DeskMonitorLogo.vue";

import { User } from "../views/Home.vue";
import { goTo, raiseToast } from "../utils";

const props = defineProps<{
	user: User;
}>();

// RESOURCES

const logout = createResource({
	url: "logout",
	onSuccess() {
		goTo("/login");
	},
	onError(error: { messages: string[] }) {
		raiseToast("error", error.messages[0]);
	},
});
</script>
