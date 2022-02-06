<template>
	<v-app id="app">
		<v-main >
			<v-container class="pa-8">
				<v-row justify="center">
					<vue-countdown
						:time="time"
						:interval="1000"
						tag="div"
						v-slot="{ days, hours, minutes, seconds, milliseconds }">
							<v-row style="width: 40vw" >
								<v-col >
									<v-row justify="center">{{ days }}</v-row>
									<v-row justify="center">Days</v-row>
								</v-col>
								<v-col>
									<v-row justify="center">{{ hours }}</v-row>
									<v-row justify="center">Hours</v-row>
								</v-col>
								<v-col>
									<v-row justify="center">{{ minutes }}</v-row>
									<v-row justify="center">Minutes</v-row>
								</v-col>
								<v-col>
									<v-row justify="center">{{ seconds }}</v-row>
									<v-row justify="center">Seconds</v-row>
								</v-col>
								<v-col>
									<v-row justify="center">{{ milliseconds }}</v-row>
									<v-row justify="center">Milliseconds</v-row>
								</v-col>
							</v-row>
					</vue-countdown>
				</v-row>

				<v-row class="mt-12" justify="center">
					<vue-countdown
						:time="time"
						:interval="1000"
						tag="div"
						style="font-size: 3vw"
						v-slot="{ days, hours, minutes, seconds }">
						<vue-countdown
						:time="time"
						:interval="51"
						tag="div"
						style="font-size: 3vw"
						v-slot="{ milliseconds }">
							<v-row >
								<v-col>
									<v-row justify="center"> {{ days }}: </v-row>
									<v-row  style="font-size:15px">days</v-row>
								</v-col>
								<v-col>
									<v-row justify="center"> {{ pad(hours, 2) }}: </v-row>
									<v-row  style="font-size:15px">hrs</v-row>
								</v-col>
								<v-col>
									<v-row justify="center"> {{ pad(minutes, 2) }}: </v-row>
									<v-row  style="font-size:15px">min</v-row>
								</v-col>
								<v-col>
									<v-row justify="center"> {{ pad(seconds, 2) }}: </v-row>
									<v-row style="font-size:15px">sec</v-row>
								</v-col>
								<v-col>
									<v-row justify="center"> {{ pad(milliseconds, 3) }} </v-row>
									<v-row  style="font-size:15px">milsecs</v-row>
								</v-col>
							</v-row>
							
						</vue-countdown>
					</vue-countdown>
				</v-row>

				<div
					class="mt-8"
				>
					<v-row
						v-for="tz in TZ"
						:key="tz"
						
					>
						<Clock
							:TZ="tz"
							:size="10"
						></Clock>
					</v-row>
				</div>
				
				<div class="white--text">{{ time }}</div>
				
			</v-container>
		</v-main>
	</v-app>
</template>

<script>
/* eslint-disable vue/no-unused-components */
/* eslint-disable vue/no-unused-vars */
import Clock from "./components/Clock.vue";
import VueCountdown from '@chenfengyuan/vue-countdown';


export default {
	name: "App",
	

	components: { 
		Clock, VueCountdown
		},

	data() {
		const now = new Date();
		const newYear = new Date(2089, 11, 16);
		return {
			TZ: ["Europe/London", "Europe/Moscow", "Asia/Tokyo"],
			time: newYear - now,
		};
	},
	methods: {	
		pad(num, size) {
			num = num.toString();
			while (num.length < size) num = "0" + num;
			return num;
		}
	}
};
</script>

<style >
* {
	/* border: 1px solid white; */
}
#app {
	background: #2a2a2a;
	color: #ffffff;
}

@font-face {
	font-family: Roboto Bold;
	src: local("Roboto Bold"), url("./fonts/Roboto-Bold.ttf");
}
@font-face {
	font-family: Roboto Regular;
	src: local("Roboto Regular"), url("./fonts/Roboto-Regular.ttf");
}
</style>