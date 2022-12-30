<script lang="ts">
	import '@skeletonlabs/skeleton/themes/theme-hamlindigo.css';
	import '@skeletonlabs/skeleton/styles/all.css';
	import '../app.postcss';
	import { AppShell, AppBar, Modal, Toast} from '@skeletonlabs/skeleton'

	// SvelteKit Imports
	import { browser } from '$app/environment';
	import { page } from '$app/stores';
	import { afterNavigate } from '$app/navigation';

	// Stores
	import { storeCurrentUrl } from '$lib/components/stores';
	import SiteSidebar from '$lib/components/SiteNavigation/SiteSidebar.svelte';
	import SiteAppBar from '$lib/components/SiteAppBar/SiteAppBar.svelte';
	import SiteDrawer from '$lib/components/SiteNavigation/SiteDrawer.svelte';
	
	afterNavigate((params: any) => {
		// Store current page route URL
		storeCurrentUrl.set($page.url.pathname);
		// Scroll to top
		const isNewPage: boolean = params.from && params.to && params.from.route.id !== params.to.route.id;
		const elemPage = document.querySelector('#page');
		if (isNewPage && elemPage !== null) {
			elemPage.scrollTop = 0;
		}
	});
</script>

<Modal />
<Toast />
<SiteDrawer />

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<SiteAppBar />
	</svelte:fragment>
	<!-- Page Route Content -->
	<svelte:fragment slot="sidebarLeft">
		<SiteSidebar class="hidden lg:grid w-[360px] overflow-hidden" />
	</svelte:fragment>

	<slot />
</AppShell>
