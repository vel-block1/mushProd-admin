<script lang="ts">
	import { getModalStore } from '@skeletonlabs/skeleton';
	import { report } from '$lib/stores/stores';
	import { onMount } from 'svelte';

	/** Exposes parent props to this component. */
	export let parent: any;

	// Local
	const modalStore = getModalStore();

	// Handle Form Submission
	function onFormSubmit(): void {
		// if ($modalStore[0].response) $modalStore[0].response('ok');
		modalStore.close();
	}

	// Base Classes
	const cBase = 'card p-4 w-modal shadow-xl space-y-4';
	const cHeader = 'text-2xl font-bold';

	let date: string;

	report.subscribe((data) => {});

	let element: any;
	onMount(() => {
		// This code will run after the component is first rendered
		element = document.getElementById('element');
		console.log(element);
	});

	// $: element = document.getElementById('element');
	// console.log(element);
	// @ts-nocheck
	function download(element: string) {
		console.log(element);

		html2pdf(element, {
			margin: 10,
			filename: 'report.pdf',
			image: { type: 'jpeg', quality: 0.98 },
			html2canvas: { scale: 2, logging: true, dpi: 192, letterRendering: true },
			jsPDFL: { unit: 'mm', format: 'a4', orientation: 'portrait' }
		});
	}
</script>

<!-- <div id="element">
	<h1>Mushprod and Humidity Tracking System Report</h1>

	<h2>System Overview</h2>
	<p><strong>System Name:</strong> [Your System Name]</p>
	<p><strong>Date of Report:</strong> [Date of Report]</p>
	<p><strong>Report Generated By:</strong> [Your Name]</p>
	<p><strong>System Location:</strong> [Location/Field]</p>
	<p><strong>System ID:</strong> [Unique System ID]</p>

	<h2>I. Weather Data</h2>

	<h3>A. Temperature and Humidity Data</h3>

	<h4>1. Current Conditions</h4>
	<p><strong>Temperature:</strong> [Current Temperature]</p>
	<p><strong>Humidity:</strong> [Current Humidity]</p>
	<p><strong>Date and Time:</strong> [Date and Time of Reading]</p>

	<h4>2. Historical Data</h4>
	<p><strong>Temperature Trends:</strong> [Graph/Chart - Temperature Trends Over Time]</p>
	<p><strong>Humidity Trends:</strong> [Graph/Chart - Humidity Trends Over Time]</p>

	<h2>II. Crop Management</h2>

	<h3>A. Planted Bags</h3>

	<h4>1. Planted Bag Inventory</h4>
	<table>
		<tr>
			<th>Total Bags Planted</th>
			<th>Crop Type</th>
			<th>Planting Date</th>
			<th>Expected Harvest Date</th>
		</tr>
		<tr>
			<td>[Total Bags Planted]</td>
			<td>[Crop Type]</td>
			<td>[Planting Date]</td>
			<td>[Expected Harvest Date]</td>
		</tr>
	</table>

	<h4>2. Bag Status</h4>
	<table>
		<tr>
			<th>Bag ID</th>
			<th>Crop Type</th>
			<th>Planting Date</th>
			<th>Status</th>
			<th>Harvest Date</th>
		</tr>
		<tr>
			<td>[Unique Bag ID]</td>
			<td>[Crop Type]</td>
			<td>[Planting Date]</td>
			<td>[Status - Growing/Harvested/Other]</td>
			<td>[Harvest Date]</td>
		</tr>
	</table>

	<div class="html2pdf__page-break" />

	<h3>B. Harvest Records</h3>

	<h4>1. Harvested Bags</h4>
	<table>
		<tr>
			<th>Total Bags Harvested</th>
			<th>Crop Type</th>
			<th>Harvest Date</th>
		</tr>
		<tr>
			<td>[Total Bags Harvested]</td>
			<td>[Crop Type]</td>
			<td>[Harvest Date]</td>
		</tr>
	</table>

	<h4>2. Bag Details</h4>
	<table>
		<tr>
			<th>Bag ID</th>
			<th>Crop Type</th>
			<th>Harvest Date</th>
			<th>Yield (lbs/kg)</th>
		</tr>
		<tr>
			<td>[Unique Bag ID]</td>
			<td>[Crop Type]</td>
			<td>[Harvest Date]</td>
			<td>[Yield in pounds/kg]</td>
		</tr>
	</table>

	<h2>III. Notification Log</h2>

	<h3>A. Recent Notifications</h3>
	<p><strong>Date and Time:</strong> [Date and Time]</p>
	<p><strong>Notification Type:</strong> [Type - Temperature Alert/Humidity Alert/Other]</p>
	<p><strong>Message:</strong> [Notification Message]</p>

	<h3>B. Notification History</h3>
	<p><strong>Date and Time:</strong> [Date and Time]</p>
	<p><strong>Notification Type:</strong> [Type - Temperature Alert/Humidity Alert/Other]</p>
	<p><strong>Message:</strong> [Notification Message]</p>

	<h2>IV. System Health</h2>

	<h3>A. System Status</h3>
	<p><strong>System Health:</strong> [Status - Good/Fair/Poor]</p>
	<p><strong>Last System Check:</strong> [Date and Time]</p>
	<p><strong>Additional Notes:</strong> [Any relevant system health information]</p>

	<h2>V. Recommendations</h2>
	<p>[Any recommendations or actions to be taken based on the data and system status]</p>

	<h2>VI. Conclusion</h2>
	<p>[Summary of the current state of the system and key takeaways]</p>
</div> -->

<!-- @component This example creates a simple form modal. -->

{#if $modalStore[0]}
	<div class="modal-example-form {cBase}">
		<header class={cHeader}>
			<div class="flex items-center justify-center">Generate Report</div>
		</header>
		<article />
		<h1 class="text-base">Do you want to generate report ?</h1>

		<!-- prettier-ignore -->
		<footer class="modal-footer {parent.regionFooter}">
			
			<button class="btn {parent.buttonPositive}" on:click={()=>download(element)}>Yes</button>
            <button class="btn {parent.buttonNeutral}" on:click={parent.onClose}
				>{parent.buttonTextCancel}</button
			>
		</footer>
	</div>
{:else}
	<div id="element">
		<h1>Mushprod and Humidity Tracking System Report</h1>

		<h2>System Overview</h2>
		<p><strong>System Name:</strong> [Your System Name]</p>
		<p><strong>Date of Report:</strong> [Date of Report]</p>
		<p><strong>Report Generated By:</strong> [Your Name]</p>
		<p><strong>System Location:</strong> [Location/Field]</p>
		<p><strong>System ID:</strong> [Unique System ID]</p>

		<h2>I. Weather Data</h2>

		<h3>A. Temperature and Humidity Data</h3>

		<h4>1. Current Conditions</h4>
		<p><strong>Temperature:</strong> [Current Temperature]</p>
		<p><strong>Humidity:</strong> [Current Humidity]</p>
		<p><strong>Date and Time:</strong> [Date and Time of Reading]</p>

		<h4>2. Historical Data</h4>
		<p><strong>Temperature Trends:</strong> [Graph/Chart - Temperature Trends Over Time]</p>
		<p><strong>Humidity Trends:</strong> [Graph/Chart - Humidity Trends Over Time]</p>

		<h2>II. Crop Management</h2>

		<h3>A. Planted Bags</h3>

		<h4>1. Planted Bag Inventory</h4>
		<table>
			<tr>
				<th>Total Bags Planted</th>
				<th>Crop Type</th>
				<th>Planting Date</th>
				<th>Expected Harvest Date</th>
			</tr>
			<tr>
				<td>[Total Bags Planted]</td>
				<td>[Crop Type]</td>
				<td>[Planting Date]</td>
				<td>[Expected Harvest Date]</td>
			</tr>
		</table>

		<h4>2. Bag Status</h4>
		<table>
			<tr>
				<th>Bag ID</th>
				<th>Crop Type</th>
				<th>Planting Date</th>
				<th>Status</th>
				<th>Harvest Date</th>
			</tr>
			<tr>
				<td>[Unique Bag ID]</td>
				<td>[Crop Type]</td>
				<td>[Planting Date]</td>
				<td>[Status - Growing/Harvested/Other]</td>
				<td>[Harvest Date]</td>
			</tr>
		</table>

		<div class="html2pdf__page-break" />

		<h3>B. Harvest Records</h3>

		<h4>1. Harvested Bags</h4>
		<table>
			<tr>
				<th>Total Bags Harvested</th>
				<th>Crop Type</th>
				<th>Harvest Date</th>
			</tr>
			<tr>
				<td>[Total Bags Harvested]</td>
				<td>[Crop Type]</td>
				<td>[Harvest Date]</td>
			</tr>
		</table>

		<h4>2. Bag Details</h4>
		<table>
			<tr>
				<th>Bag ID</th>
				<th>Crop Type</th>
				<th>Harvest Date</th>
				<th>Yield (lbs/kg)</th>
			</tr>
			<tr>
				<td>[Unique Bag ID]</td>
				<td>[Crop Type]</td>
				<td>[Harvest Date]</td>
				<td>[Yield in pounds/kg]</td>
			</tr>
		</table>

		<h2>III. Notification Log</h2>

		<h3>A. Recent Notifications</h3>
		<p><strong>Date and Time:</strong> [Date and Time]</p>
		<p><strong>Notification Type:</strong> [Type - Temperature Alert/Humidity Alert/Other]</p>
		<p><strong>Message:</strong> [Notification Message]</p>

		<h3>B. Notification History</h3>
		<p><strong>Date and Time:</strong> [Date and Time]</p>
		<p><strong>Notification Type:</strong> [Type - Temperature Alert/Humidity Alert/Other]</p>
		<p><strong>Message:</strong> [Notification Message]</p>

		<h2>IV. System Health</h2>

		<h3>A. System Status</h3>
		<p><strong>System Health:</strong> [Status - Good/Fair/Poor]</p>
		<p><strong>Last System Check:</strong> [Date and Time]</p>
		<p><strong>Additional Notes:</strong> [Any relevant system health information]</p>

		<h2>V. Recommendations</h2>
		<p>[Any recommendations or actions to be taken based on the data and system status]</p>

		<h2>VI. Conclusion</h2>
		<p>[Summary of the current state of the system and key takeaways]</p>
	</div>
{/if}

<style>
	h1 {
		text-align: center;
	}

	h2,
	h3,
	h4 {
		margin-top: 20px;
	}

	p {
		margin: 5px 0;
	}

	table {
		width: 100%;
		border-collapse: collapse;
	}

	table,
	th,
	td {
		border: 1px solid #333;
	}

	th,
	td {
		padding: 8px;
		text-align: left;
	}
</style>