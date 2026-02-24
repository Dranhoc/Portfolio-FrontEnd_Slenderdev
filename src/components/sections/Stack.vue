<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import CabinCanvas from '@/components/CabinCanvas.vue';
import GlitchAnimation from '@/components/GlitchAnimation.vue';

const magnifierKey = ref(0);
let resizeObserver: ResizeObserver;

onMounted(() => {
	setTimeout(() => {
		const illustrationElement = document.querySelector('.s-stack__illustration') as HTMLElement;
		if (illustrationElement) {
			let oldWidth = illustrationElement.getBoundingClientRect().width;
			let oldHeight = illustrationElement.getBoundingClientRect().height;

			resizeObserver = new ResizeObserver((entries) => {
				for (const entry of entries) {
					const { width, height } = entry.contentRect;
					if (width > 0 && height > 0) {
						const widthChange = Math.abs(width - oldWidth) / oldWidth;
						const heightChange = Math.abs(height - oldHeight) / oldHeight;

						if (widthChange > 0.15 || heightChange > 0.15) {
							magnifierKey.value++;
							oldWidth = width;
							oldHeight = height;
						}
					}
				}
			});
			resizeObserver.observe(illustrationElement);
		}
	}, 500);
});

onBeforeUnmount(() => {
	if (resizeObserver) {
		resizeObserver.disconnect();
	}
});
</script>

<template>
	<section class="s-stack">
		<div class="s-stack__content">
			<div class="s-stack__stack">
				<h3><GlitchAnimation text="THINGS I ARGUE WITH DAILY." /></h3>
				<ul>
					<li>Vue</li>
					<li>React</li>
					<li>Angular</li>
					<li>Caffeine</li>
					<li>Node.js</li>
					<li>TailwindCSS</li>
					<li>VITE</li>
					<li>Linkedin bots</li>
					<li>JavaScript</li>
					<li>Express</li>
					<li>ChatGemini</li>
					<li>TypeScript</li>
					<li>Supabase</li>
					<li>HTML</li>
					<li>Paracetamol</li>
					<li>SCSS</li>
					<li>PostgresSQL</li>
					<li>Nest.js</li>
					<li>Git</li>
					<li>Postman</li>
					<li>Graude</li>
					<li>Figma</li>
					<li>Access</li>
					<li>Excel</li>
					<li>Slenderdev near the shack</li>
					<li>Python</li>
					<li>My cat</li>
					<li>CSS</li>
					<li>Safari without a Mac</li>
				</ul>
			</div>
			<div class="s-stack__illustration">
				<CabinCanvas :key="magnifierKey" />
			</div>
		</div>
	</section>
</template>

<style scoped lang="scss">
.s-stack {
	position: relative;
	background-color: var(--bg-primary);
	z-index: 1;

	&__content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;
		min-height: calc(100vh - 8vh);
		min-height: calc(100dvh - 8dvh);
		gap: 40px;
		background-color: var(--bg-primary);
		z-index: 1;
		@apply md:flex-row px-20 pb-60 md:p-40;
		@screen 4xl {
			min-height: unset;
			height: calc(100vh - 8vh);
			height: calc(100dvh - 8dvh);
			max-height: 1200px;
		}
	}

	&__illustration {
		display: flex;
		justify-content: center;
		@apply md:w-[50%];
	}

	&__stack {
		display: flex;
		flex-direction: column;
		color: var(--text-secondary);
		background-color: var(--bg-primary);
		flex-shrink: 0;
		width: 100%;
		@apply md:w-[50%];
		ul {
			display: flex;
			flex-wrap: wrap;
			gap: 10px;
			margin-top: 20px;
			@apply md:mt-40 2xl:gap-20;
			li {
				width: fit-content;
				border: 1px solid rgb(172, 172, 172);
				padding: 5px;
				line-height: 1;
				@apply 2xl:p-10;
			}
		}
	}
}
</style>
