<template>
	<div class="home">
		<b-container>
			<b-row v-for="(o, i) in b" :key="i">
				<b-col v-for="(obj, j) in o" :key="j">
					<Card :name="obj.name" :room="obj.room" :team="obj.slot">
					</Card>
				</b-col>
			</b-row>
		</b-container>
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
		for(let i = 0; i < n; i++) {
			this.a.push(i);
		}
		this.a = this.shuffle(this.a);
		this.addRoomTag();
	}

	addRoomTag() {
		const num1s = Math.ceil(this.a.length/2);
		const num2s = this.a.length - num1s;
		const R1 = this.a.slice(0, num1s);
		const R2 = this.a.slice(num1s);
		let slot = 1
		for (const i in R1) {
			R1[i] = {
				name: String.fromCharCode(65 + R1[i]),
				room: 1,
				slot: slot
			};
			slot++;
		}
		slot = 1;
		for (const i in R2) {
			R2[i] = {
				name: String.fromCharCode(65 + R2[i]),
				room: 2,
				slot: slot
			};
			slot++;
		}
		// this.b = this.b.sort(() => Math.random() - 0.5);
		this.b = this.shuffle(R1.concat(R2));
		const n = 5; //tweak this to add more items per line

		const result = new Array(Math.ceil(this.b.length / n))
		.fill(undefined, undefined, undefined)
		.map(_ => this.b.splice(0, n))

		this.b = result;

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