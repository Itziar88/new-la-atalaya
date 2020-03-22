<template>
	<button :class="buttonClass" class="WButton" @click="$emit('click')">
		<slot />
	</button>
</template>

<script>
import VueTypes from 'vue-types'

export default {
	name: 'WButton',
	props: {
		disabled: VueTypes.bool.def(false)
	},
	computed: {
		buttonClass() {
			return [
				{
					disabled: this.disabled
				}
			]
		}
	}
}
</script>

<style lang="scss" scoped>
@import '@/theme/theme.scss';

.WButton {
	position: relative;
	padding: 12px 24px 14px 24px;
	border-radius: 24px;
	border: 1px solid $primary;
	color: $primary;
	background: transparent;
	font-size: $font-size;
	line-height: 22px;
	outline: none;
	cursor: pointer;
	transition: all 0.4s ease-in-out;

	&:hover {
		background-color: $primary;
		color: $white;
	}
	&:active,
	&.active {
		background-color: rgba($primary, 0.8);
	}
	&:focus {
		outline: none;
	}
	&.disabled {
		background-color: rgba($grey-02, 0.7);
		border-color: rgba($grey-02, 0.7);
		color: $white;
		&:hover {
			cursor: default;
		}
	}
}
</style>
