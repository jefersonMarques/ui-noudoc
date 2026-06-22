<script lang="ts">
	import './layout.css';

	const { children } = $props();
</script>

<div class="style-vega min-h-screen bg-background text-foreground">
	{@render children()}
</div>
