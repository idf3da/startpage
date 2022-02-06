<template>
	<v-main>
		<v-col>
			<v-row justify="center">
				<Clock-Analog
					color="
			black"
					:time="time"
					border="1px solid"
					:bg="white"
					:size="size+'vw'"
				>
				</Clock-Analog>
			</v-row>

			<v-row justify="center">
				<v-card
					id="city"
					:style="`--size: this.size+'
					vh'`"
					class="ma-0"
					:min-width="size+'vw'"
					elevation="6"
				>
				

					<p class="text-wrap text-center mb-1 mt-1 ml-3 mr-3">
						{{ getCity() }}
					</p>

				</v-card>
			</v-row>
		</v-col>

	</v-main>
</template>

<script>
import ClockAnalog from "vue-clock2";

export default {
	name: "Clock",

	components: { ClockAnalog },

	props: ["TZ", "size"],

	data() {
		return {
			interval: null,
			time: null,
			white: "white",
			black: "#292A2D",
		};
	},
	methods: {
		getCity() {
			return this.TZ.split("/")[1].toUpperCase();
		},
	},
	beforeDestroy() {
		// prevent memory leak
		clearInterval(this.interval);
	},
	created() {
		this.interval = setInterval(() => {
			this.time = Intl.DateTimeFormat("ru-RU", {
				timeZone: this.TZ,
				hour: "numeric",
				minute: "numeric",
				second: "numeric",
			}).format();
		}, 1000);
	},
};
</script>

<style lang="scss">
* {
	// border: 1px dotted black;
}

#city {
	font-family: "Roboto Medium";
	border: 1px solid black;
	font-size: var(--size);
}
</style>