<template>
    <div>
        <div class="grid grid-flow-row grid-cols-3 grid-rows-3 gap-4">
            <div :key="json.id" v-for="json in data" class="max-w-sm rounded overflow-hidden shadow-lg">
                <img class="w-full" v-bind:src="json.url">
                <div class="px-6 py-4">
                    <div class="font-bold text-xl mb-2">{{ json.title }}</div>
                    <p class="text-gray-700 text-base">{{ json.id }}</p>
                    <input class="mr-2 leading-tight" type="checkbox" @input="$emit('click', $event.target.value)"> check me for select
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "ListRendering",
    props: ["data", "value"],
    model: {
        prop: "input",
        event: "click",
    },
};
</script>