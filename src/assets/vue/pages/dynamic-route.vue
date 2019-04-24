<template>
	<f7-page>
		<f7-navbar title="Dynamic Route" back-link="Back" sliding></f7-navbar>
		<f7-block inner>
			<ul>
				
					<ul>
						<li v-for="(value, key) in $route.params" :key="'param-' + key"><b>{{key}}:</b> {{value}}</li>
					</ul>
				</li>
						</ul>
		</f7-block>
		<f7-block inner>
			<f7-link @click="$router.back()">Go back via Router API</f7-link>
		</f7-block>
	
	</f7-page>
</template>

<script>
	export default {}
</script>