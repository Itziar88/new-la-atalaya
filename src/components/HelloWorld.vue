<template>
	<div class="hello">
		<WText typo="h1">Texto</WText>
		<WButton>Texto</WButton>
	</div>
</template>

<script>
import { WText, WButton } from '@/components'

export default {
	name: 'HelloWorld',
	components: {
		WText,
		WButton
	}
}
</script>
