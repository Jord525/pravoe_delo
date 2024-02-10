<script>
export default {
    props: ["managers2", "selectedManager2"],
    data() {
        return {
            selectedValue2: "",
        };
    },
    methods: {
        emitEvent() {
            this.$emit("child-event2", this.selectedValue2);
        },
    },
};
</script>

<template>
    <select
        v-model="selectedValue2"
        @change="emitEvent"
        class="block h-10 p-2 mb-1 ml-4 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
    >
        <option disabled value="">{{ selectedManager2.name }}</option>
        <option v-for="(option, i, b) in managers2">
            {{ i }} : {{ option }}
        </option>
    </select>
</template>
