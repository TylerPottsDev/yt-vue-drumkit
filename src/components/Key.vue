<template>
	<button :class="`key ${clicked ? 'clicked' : ''}`" @click="play">
		{{ sound.letter }}
	</button>
</template>

<script>
export default {
	name: 'key',
	props: ['sound'],
	data () {
		return {
			clicked: false
		}
	},
	methods: {
		play() {
			this.clicked = true;
			new Audio(this.sound.audio).play();

			setTimeout(() => {
				this.clicked = false;
			}, 200);
		}
	},
	mounted () {
		document.addEventListener('keydown', (e) => {
			if (e.key.toLowerCase() === this.sound.letter.toLowerCase()) {
				this.play();
			}
		});
	}
}
</script>

<style>
	button {
		appearance: none;
		background: none;
		outline: none;
		border: none;
		cursor: pointer;

		display: block;
		width: 100px;
		height: 100px;
		font-size: 48px;
		margin: 0 0.5rem;

		color: #FFF;
		font-weight: 700;
		background-color: crimson;
		border-radius: 1rem;

		transition: 0.4s;
	}

	button:hover {
		opacity: 0.7;
		transform: scale(0.95);
	}

	button:active, button.clicked {
		transform: scale(1.1);
		box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.7);
	}
</style>