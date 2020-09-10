<template>
	<div style="display: inline-block; width: 120px; padding: 10px;">
		<div v-if="!toggle">
			<button @click.prevent="toggle=!toggle">{{name}}</button>
		</div>
		<div v-else class="room-div">
			<strong><span style="color:red;">R</span> {{room}} <span style="color:blue;">T</span> {{team}}</strong>
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

.room-div {
	text-align: center;
	margin: 10px;
}
</style>
<script lang="ts">
import { Vue, Component, Prop, Provide } from 'vue-property-decorator';

@Component
export default class Card extends Vue {
	@Prop() name?: string;
	@Prop() room?: number;
	@Prop() team?: number;
	toggle = false;
}
</script>