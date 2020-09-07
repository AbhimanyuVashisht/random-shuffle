<template>
  <div class="home">
		<Card v-for="(obj, i) in b" :key="i" :name="obj.name" :room="obj.room">
			{{obj.name}}
		</Card>
  </div>
</template>
<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import Card from '@/components/Card.vue';

@Component({
	components: {
		Card
	}
})
export default class Home extends Vue {
	n: any = 0;
	a: Record<string, any> = [];
	b: Record<string, any> = [];

	created() {
		if (this.$route.query.q) {
			this.n = this.$route.query.q;
			this.process(this.n);
		}
	}

	process(n: any) {
		for(let i = 1; i <= n; i++) {
			this.a.push(i);
		}
		this.b = this.a.sort(() => Math.random() - 0.5);
		this.addRoomTag();
	}

	addRoomTag() {
		const num1s = Math.floor(this.a.length/2);
		const num2s = this.a.length - num1s;
		for (let i = 1; i <= num1s; i++) {
			const indexOfEl = this.b.indexOf(this.a[i - 1]);
			this.b[indexOfEl] = {
				name: String.fromCharCode(64 + this.b[indexOfEl]),
				room: 1
			};
		}
		for (let i = num1s + 1; i <= this.a.length; i++) {
			const indexOfEl = this.b.indexOf(this.a[i - 1]);
			this.b[indexOfEl] = {
				name: String.fromCharCode(64 + this.b[indexOfEl]),
				room: 2
			};
		}
		// this.b = this.b.sort(() => Math.random() - 0.5);
		this.b = this.shuffle(this.b);
	}
	shuffle(arra1: Record<string, any>) {
		let ctr = arra1.length, temp, index;

		// While there are elements in the array
		while (ctr > 0) {
			// Pick a random index
			index = Math.floor(Math.random() * ctr);
			// Decrease ctr by 1
			ctr--;
			// And swap the last element with it
			temp = arra1[ctr];
			arra1[ctr] = arra1[index];
			arra1[index] = temp;
		}
		return arra1;
	}
}
</script>