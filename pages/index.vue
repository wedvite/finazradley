<template>
	<section id="wedvite" class="container" v-if="showPage">
		<!-- <keep-alive> -->
		<main-content v-if="check(sectionStatus.main)" />
		<invitation v-if="check(sectionStatus.invitation)" />
		<tentative v-if="check(sectionStatus.tentative)" />
		<doa v-if="check(sectionStatus.doa)"></doa>

		<div id="notice" class="section">
			<div data-aos="zoom-in" data-aos-offset="300" class="text">PENTING</div>
			<ul>
				<li data-aos="fade-right" data-aos-offset="300">Sila bawa bersama kad touch n go anda untuk kemudahan parkir di 3 Towers.</li>
				<li data-aos="fade-right" data-aos-offset="300">Parkir tetamu hanya boleh di park di tempat letak kenderaan di Tower 2 dan Tower 3.</li>
				<li data-aos="fade-right" data-aos-offset="300">Sila patuhi waktu kehadiran yang telah ditetapkan bagi melancarkan perjalanan majlis.</li>
				<li data-aos="fade-right" data-aos-offset="300">Sila tekan butang RSVP di bawah dan sah kan kehadiran anda sebelum 17 September 2023. Kerjasama daripada anda amatlah kami hargai. Terima kasih</li>
			</ul>
		</div>

		<countdown v-if="check(sectionStatus.countdown)" />
		<social v-if="check(sectionStatus.social)" />
		<wishlist v-if="check(sectionStatus.wishlist)" />
		<rsvp v-if="check(sectionStatus.rsvp)" />
		<app-footer></app-footer>
		<!-- </keep-alive> -->
	</section>
</template>

<script>
import "bulma-modal-fx/dist/js/modal-fx.min";
import { userData as data, themes } from "~/wedvite.config.js";

import MainContent from "~/components/MainContent";
import Invitation from "~/components/Invitation";
import Tentative from "~/components/Tentative";
import Doa from "~/components/Doa";
import Countdown from "~/components/Countdown";
import Social from "~/components/Social";
import Wishlist from "~/components/Wishlist";
import Rsvp from "~/components/Rsvp";
import Footer from "~/components/Footer";
import { mapState } from "vuex";

export default {
	// asyncData({ store }) {
	//   return store.dispatch("getInfo");
	// },
	components: {
		MainContent,
		Invitation,
		Tentative,
		Doa,
		Countdown,
		Social,
		Wishlist,
		Rsvp,
		AppFooter: Footer,
	},
	computed: {
		...mapState({
			showPage: (state) => state.showPage,
			sectionStatus: (state) => state.info.section_status || {},
		}),
	},
	async created() {
		let theme = themes.includes(this.$route.query.t)
			? this.$route.query.t
			: null;

		this.$store.dispatch("getInfo", {
			info: data,
			// lang: data.lang
			overrideTheme: theme || data.theme,
		});
	},
	methods: {
		check(s) {
			return s || s === undefined ? true : false;
		},
	},
};
</script>

<style lang="scss">
@import "~assets/scss/var.scss";
@import url($font-url);

#wedvite {
	margin-bottom: 3rem;
	overflow-x: hidden !important;

	.modal {
		max-width: 520px;
	}

  &.container,
	.container {
		width: 100%;
		max-width: 520px !important;
		font-family: $primary-font !important;
	}
}

@media only screen and (min-width: 520px) {
	#wedvite {
		border-right: #ddd 1px solid;
		border-left: #ddd 1px solid;
	}
}
</style>
