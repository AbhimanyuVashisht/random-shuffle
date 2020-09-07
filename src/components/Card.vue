<template>
	<div>
		<div v-if="!toggle">
			<button @click.prevent="toggle=!toggle">{{name}}</button>
		</div>
		<div v-else>
			Your room number is {{room}} :P
		</div>
	</div>
</template>
<style>
button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 10px;
}
</style>
<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';

@Component
export default class Card extends Vue {
	@Prop() name?: string;
	@Prop() room?: number;
	toggle = false;
}
</script>