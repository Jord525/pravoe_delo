<script>
export default {
    props: ["modelValue", "inputType", "placeholder"],
    emits: ["update:modelValue"],
};
</script>

<template>
    <input
        class="w16 h-10 px-3 mb-2 mt-2 mr-2 text-base text-gray-700 placeholder-gray-600 border rounded-lg focus:shadow-outline"
        :type="inputType"
        :placeholder="placeholder"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
    />
</template>
