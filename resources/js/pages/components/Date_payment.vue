<script>
export default {
    props: ["data", "modalData"],
    methods: {
        closePopUp() {
            this.$emit("closePopup");
        },
    },
    mounted() {},
};
</script>

<template>
    <div>
        <div
            id="default-modal"
            tabindex="-1"
            class="overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full"
        >
            <div
                class="absolute left-1/2 right-1/2 -translate-x-1/2 translate-y-1/2 p-4 w-full max-w-2xl max-h-full"
            >
                <div class="relative bg-white rounded-lg shadow dark:bg-white">
                    <div
                        class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600"
                    >
                        <h3
                            class="text-xl font-semibold text-white dark:text-gray-700"
                        >
                            Модальное окно
                        </h3>
                        <button
                            @click="closePopUp"
                            type="button"
                            class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                        >
                            <svg
                                class="w-3 h-3"
                                xmlns="http://www.w3.org/2000/svg"
                                fill="none"
                                viewBox="0 0 14 14"
                            >
                                <path
                                    stroke="currentColor"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"
                                />
                            </svg>
                            <span @click="closePopUp" class="sr-only"
                                >Close modal</span
                            >
                        </button>
                    </div>
                    <div
                        v-for="data in modalData.list_full_remmitances"
                        class="p-4 md:p-5 space-y-4"
                    >
                        {{ data.amount }} - {{ data.payed_at }}
                    </div>
                    <div
                        class="flex items-center p-4 md:p-5 border-t border-gray-200 rounded-b dark:border-gray-600"
                    >
                        <button
                            @click="closePopUp"
                            type="button"
                            class="ms-3 text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-blue-300 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600"
                        >
                            Закрыть
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
