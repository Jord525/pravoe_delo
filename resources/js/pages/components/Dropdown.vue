<script>
export default {
    props: ["managers", "selectedManager"],
    data() {
        return {
            selectedValue: "",
        };
    },
    methods: {
        emitEvent() {
            this.$emit("child-event", this.selectedValue);
        },
    },
};
</script>

<template>
    <select
        v-model="selectedValue"
        @change="emitEvent"
        class="block h-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-white dark:border-gray-400 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
    >
        <option disabled value="">{{ selectedManager.name }}</option>
        <option v-for="(option, i) in managers">{{ i }} : {{ option }}</option>
    </select>
</template>
