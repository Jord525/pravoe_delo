<script>
export default {
    props: ["role"],
};
</script>
<template>
    <div>
        <thead>
            <tr class="border flex">
                <th
                    v-if="role === 'Lawyer'"
                    scope="col"
                    class="px-6 w-60 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Офис и менеджер
                </th>
                <th
                    v-else
                    scope="col"
                    class="px-6 w-56 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Менеджер
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Юрист
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    ФИО клиента
                </th>
                <th
                    v-if="role === 'Lawyer'"
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Программа
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Дата регистрации
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    План
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Стоимость
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    В месяц
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Дата оплаты
                </th>
                <th
                    scope="col"
                    class="px-6 w-36 py-4 whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                >
                    Дата передачи
                </th>
            </tr>
        </thead>
    </div>
</template>
