<script>
	import { Route ,Router} from "svelte-navigator";
	import index from "./pages/index.svelte"
	import add from "./pages/add.svelte"
	import check from "./pages/check.svelte"

</script>

<main>
	<Router>
	
		<Route default component={index}>
		</Route>
		<Route path="add" component={add} >
		</Route>
		<Route path="check" component={check} >
		</Route>
	</Router>
</main>

<style>
</style>
