<script>
import Table_head from "./components/Table_head.vue";
import Dropdown from "./components/Dropdown.vue";
import Filter from "./components/Filter.vue";
import Date_payment from "./components/Date_payment.vue";
import Pagination from "./components/Pagination.vue";
import { Link } from "@inertiajs/inertia-vue3";
import Lawyer from "./components/Lawyer.vue";
export default {
    components: {
        Table_head,
        Dropdown,
        Filter,
        Date_payment,
        Pagination,
        Link,
        Lawyer,
    },
    data() {
        return {
            table: [],
            clientId: "",
            office: "",
            manager: "",
            lawyer: "",
            isVisible: false,
            modal: "",
            date1: "",
            date2: "",
            page: "",
            first_date: "",
            second_date: "",
        };
    },
    props: ["payPlanItem", "role", "offices", "managers", "lawyers"],

    methods: {
        saveFirstDate(id) {
            this.$inertia.post("/update-data", {
                id: id.id,
                first_date: id.program_first_date,
            });
        },
        saveSecondDate(id) {
            console.log(id.id);
            this.$inertia.post("/update-data", {
                id: id.id,
                second_date: id.program_second_date,
            });
        },
        modalData(data) {
            this.modal = data;
            this.isVisible = true;
        },
        selectManager(id, data) {
            const index = Number(data.split("").splice(0, 1).join(""));
            console.log(id);
            this.$inertia.post("/update-data", {
                id: id,
                manager_id: index,
            });
        },
        updateClient(id) {
            console.log(id);
            this.$inertia.post("/update-data", {
                id: id.id,
                name: id.client_name,
            });
        },
        // selectlawyer(id, data) {
        //     const index = Number(data.split("").splice(0, 1).join(""));
        //     console.log(id);
        //     this.$inertia.post("/update-data", {
        //         id: id,
        //         lawyer_id: index,
        //     });
        // },
        logout() {
            this.$inertia.post("logout");
        },
        getFiltered() {
            this.$inertia.get(
                `/table?page=${payPlanItem.current_page}&office=`
            );
        },
        getClientId() {
            this.$inertia.get(
                `/table?client_id=${this.clientId}&page=${this.page}`
            );
        },
        getOffice() {
            this.$inertia.get(`/table?office=${this.office}&page=${this.page}`);
        },
        getManager() {
            this.$inertia.get(
                `/table?manager_id=${this.manager}&page=${this.page}`
            );
        },
        getLawyer() {
            this.$inertia.get(
                `/table?lawyer_id=${this.lawyer}&page=${this.page}`
            );
        },
        filterDate() {
            this.$inertia.get(
                `/table?dates_transfer[]=${this.date1}&dates_transfer[]=${this.date2}`
            );
        },
        filterFirsSecondDate() {
            this.$inertia.get(
                `/table?dates_pay[]=${this.first_date}&dates_pay[]=${this.second_date}`
            );
        },
    },

    mounted() {},
};
</script>
<template>
    <span
        >ваша роль - {{ role }}
        <button
            @click="logout"
            class="select-none w-32 h-11 flex flex-wrap content-center justify-center rounded-lg bg-gradient-to-tr from-white-900 to-white-800 text-center align-middle font-sans text-xs font-bold uppercase text-black-200 shadow-md shadow-gray-900/10 transition-all hover:shadow-lg hover:shadow-gray-900/20 active:opacity-[0.85] disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none"
        >
            logout
        </button>
    </span>

    <div class="flex w-44 flex-col ml-1 lg:flex-row">
        <Filter
            v-model="clientId"
            @change="getClientId"
            placeholder="клиент id"
            inputType="number"
        />
        <Filter
            v-model="office"
            @change="getOffice"
            placeholder="офис"
            inputType="text"
        />
        <Filter
            v-model="manager"
            @change="getManager"
            placeholder="менеджер"
            inputType="text"
        />
        <Filter
            v-model="lawyer"
            @change="getLawyer"
            placeholder="адвокат"
            inputType="text"
        />
    </div>
    <form class="flex items-center" @submit.prevent="filterDate">
        <button
            class="select-none w-32 h-11 flex flex-wrap content-center justify-center rounded-lg bg-gradient-to-tr from-white-900 to-white-800 text-center align-middle font-sans text-xs font-bold uppercase text-black-200 shadow-md shadow-gray-900/10 transition-all hover:shadow-lg hover:shadow-gray-900/20 active:opacity-[0.85] disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none"
            @click="filterDate"
        >
            фильтр
        </button>
        <input
            v-model="date1"
            type="date"
            class="w16 h-10 px-3 mb-2 mt-2 text-base text-gray-700 placeholder-gray-600 border rounded-lg focus:shadow-outline"
        />
        -
        <input
            v-model="date2"
            type="date"
            class="w16 h-10 px-3 mb-2 mt-2 text-base text-gray-700 placeholder-gray-600 border rounded-lg focus:shadow-outline"
        />
        <span>дата передачи</span>
    </form>
    <form class="flex items-center" @submit.prevent="filterFirsSecondDate">
        <button
            class="select-none w-32 h-11 flex flex-wrap content-center justify-center rounded-lg bg-gradient-to-tr from-white-900 to-white-800 text-center align-middle font-sans text-xs font-bold uppercase text-black-200 shadow-md shadow-gray-900/10 transition-all hover:shadow-lg hover:shadow-gray-900/20 active:opacity-[0.85] disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none"
            @click=""
        >
            фильрт
        </button>
        <input
            v-model="first_date"
            class="w-12 h-10 px-3 mb-2 mt-2 text-base text-gray-700 placeholder-gray-600 border rounded-lg focus:shadow-outline"
        />
        -
        <input
            v-model="second_date"
            class="w-12 h-10 px-3 mb-2 mt-2 text-base text-gray-700 placeholder-gray-600 border rounded-lg focus:shadow-outline"
        />
        Дата оплаты
    </form>
    <Link
        class="class=&quot;select-none mb-3 w-32 h-11 flex flex-wrap content-center justify-center rounded-lg bg-gradient-to-tr from-white-900 to-white-800 text-center align-middle font-sans text-xs font-bold uppercase text-black-200 shadow-md shadow-gray-900/10 transition-all hover:shadow-lg hover:shadow-gray-900/20 active:opacity-[0.85] disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none&quot;"
        href="/table?page=1"
        >reset all</Link
    >
    <Table_head :role="role" />
    <tbody
        v-for="(data, index) in payPlanItem.data"
        class="transition border-collapse duration-700 translate-x-0 divide-y divide-gray-200 dark:divide-gray-700"
    >
        <tr class="border flex">
            <td
                class="flex items-center justify-end w-60 whitespace-nowrap text-center text-sm font-medium text-white-800"
            >
                <div v-if="role == 'Lawyer'">{{ data.manager.office }}</div>
                -МПП -
                <span>
                    <Dropdown
                        @child-event="selectManager(data.id, $event)"
                        v-if="role == 'Lawyer'"
                        :managers="managers"
                        :selectedManager="data.manager"
                    /><span v-else>{{ data.manager.name }}</span></span
                >
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.lawyer.name }}
                <!--<lawyer
                    @child-event2="selectlawyer(data.id,$event)"
                    :managers2='lawyers'
                    :selectedManager2='data.lawyer' />-->
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                <input
                    @keyup.enter="updateClient(data)"
                    class="w-37 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                    v-model="data.client_name"
                />
            </td>
            <td
                v-if="role == 'Lawyer'"
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.program_type }}
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.date_register }}
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.program_plan }}/{{ data.all_payments }}
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.program_price }}/{{ data.all_payments }}
            </td>
            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.program_payment_per_month }}
                <button
                    @click="modalData(data)"
                    data-ripple-light="true"
                    data-dialog-target="dialog"
                    class="select-none w-36 flex flex-wrap content-center justify-center rounded-lg bg-gradient-to-tr from-white-900 to-white-800 py-3 px-6 text-center align-middle font-sans text-xs font-bold uppercase text-black-200 shadow-md shadow-gray-900/10 transition-all hover:shadow-lg hover:shadow-gray-900/20 active:opacity-[0.85] disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none"
                >
                    открыть
                </button>
            </td>
            <td
                v-if="(role = 'Lawyer')"
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                <input
                    @keyup.enter="saveFirstDate(data)"
                    class="w-14 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                    type="number"
                    v-model="data.program_first_date"
                />
                <input
                    @keyup.enter="saveSecondDate(data)"
                    class="w-14 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
                    type="number"
                    v-model="data.program_second_date"
                />
            </td>
            <td
                v-else
                class="class=&quot;w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200&quot;"
            >
                {{ data.program_first_date }} {{ program_second_date }}
            </td>

            <td
                class="w-36 flex flex-wrap content-center justify-center whitespace-nowrap text-center text-sm font-medium text-gray-800 dark:text-black-200"
            >
                {{ data.client_handover_date }}
            </td>
        </tr>
    </tbody>
    <Date_payment
        :modalData="modal"
        :data="payPlanItem.data"
        @closePopup="isVisible = false"
        v-if="isVisible"
    />
    <button @click="logout">logout</button>
    <Pagination
        class="mb-2 mt-2 ml-2"
        :next="payPlanItem.next_page_url"
        :prev="payPlanItem.prev_page_url"
    />
</template>
