<script>
export default {
    data() {
        return {
            data: {
                email: "",
                password: "",
            },
        };
    },
    methods: {
        submit() {
            this.$inertia.post("/login", this.data);
        },
    },
};
</script>
<template>
    <div>
        <form @submit.prevent="submit()">
            <div style="height: 70vh" class="flex justify-center items-center">
                <div class="w-1/4">
                    <div class="mb-6">
                        <label
                            for="email"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Ваш email</label
                        >
                        <input
                            v-model="data.email"
                            type="email"
                            id="email"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="email"
                        />
                    </div>
                    <div class="mb-6">
                        <label
                            for="password"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Ваш пароль</label
                        >
                        <input
                            v-model="data.password"
                            type="password"
                            id="password"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                        />
                    </div>

                    <button
                        type="submit"
                        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                    >
                        Вход
                    </button>
                </div>
            </div>
        </form>
    </div>
</template>
