<!--
Copyright: Ankitects Pty Ltd and contributors
License: GNU AGPL, version 3 or later; http://www.gnu.org/licenses/agpl.html
-->
<script context="module" lang="ts">
    export interface Choice<T> {
        label: string;
        value: T;
    }
</script>

<script lang="ts">
    import Select from "./Select.svelte";
    import SelectOption from "./SelectOption.svelte";

    type T = $$Generic;

    export let value: T;
    export let choices: Choice<T>[] = [];
    export let disabled: boolean = false;
    export let disabledChoices: T[] = [];

    $: label = choices.find((c) => c.value === value)?.label;
</script>

<Select bind:value {label} {disabled}>
    {#each choices as { label: optionLabel, value: optionValue }}
        <SelectOption
            value={optionValue}
            disabled={disabledChoices.includes(optionValue)}
        >
            {optionLabel}
        </SelectOption>
    {/each}
</Select>
