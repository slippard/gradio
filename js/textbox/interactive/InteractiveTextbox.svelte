<svelte:options accessors={true} />

<script lang="ts">
	import TextBox from "../shared";
	import { Block } from "@gradio/atoms";
	import { StatusTracker } from "@gradio/statustracker";
	import type { LoadingStatus } from "@gradio/statustracker";

	export let label = "Textbox";
	export let info: string | undefined = undefined;
	export let elem_id = "";
	export let elem_classes: string[] = [];
	export let visible = true;
	export let value = "";
	export let lines: number;
	export let placeholder = "";
	export let show_label: boolean;
	export let max_lines: number;
	export let type: "text" | "password" | "email" = "text";
	export let container = true;
	export let scale: number | null = null;
	export let min_width: number | undefined = undefined;
	export let show_copy_button = false;
	export let loading_status: LoadingStatus | undefined = undefined;
	export let value_is_output = false;
	export let rtl = false;
	export let text_align: "left" | "right" | undefined = undefined;
	export let autofocus = false;
</script>

<Block
	{visible}
	{elem_id}
	{elem_classes}
	{scale}
	{min_width}
	allow_overflow={false}
	padding={container}
>
	{#if loading_status}
		<StatusTracker {...loading_status} />
	{/if}

	<TextBox
		bind:value
		bind:value_is_output
		{label}
		{info}
		{show_label}
		{lines}
		{type}
		{rtl}
		{text_align}
		max_lines={!max_lines ? lines + 1 : max_lines}
		{placeholder}
		{show_copy_button}
		{autofocus}
		{container}
		on:change
		on:input
		on:submit
		on:blur
		on:select
		on:focus
	/>
</Block>
