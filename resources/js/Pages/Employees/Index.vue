<template>
    <AuthenticatedLayout>
        <!-- Title -->
        <Head title="Companies" />

        <template #header>
            <h2
                class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight"
            >
                Employees
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="flex justify-end mb-6">
                    <Link :href="route('employees.create')">
                        <PrimaryButton>Create Employee</PrimaryButton>
                    </Link>
                </div>
                <div
                    class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg pb-2"
                >
                    <table class="w-full">
                        <tr>
                            <th class="text-white p-4 text-left">No</th>
                            <th class="text-white p-4 text-left">Name</th>
                            <th class="text-white p-4 text-left">Email</th>
                            <th class="text-white p-4 text-left">Phone</th>
                            <th class="text-white p-4 text-left">Company</th>
                            <th class="text-white p-4">Actions</th>
                        </tr>
                        <tr
                            v-for="(item, index) in employees.data"
                            :key="item.id"
                        >
                            <td class="text-white px-4 py-2">
                                {{
                                    index +
                                    1 +
                                    (employees.current_page - 1) * 10
                                }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ item.first_name }} {{ item.last_name }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ item.email }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ item.phone }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ item.company.name || "" }}
                            </td>
                            <td
                                class="text-white px-4 py-2 space-x-4 text-center"
                            >
                                <Link :href="route('employees.show', item.id)">
                                    <PrimaryButton>Show</PrimaryButton>
                                </Link>
                                <Link :href="route('employees.edit', item.id)">
                                    <PrimaryButton>Edit</PrimaryButton>
                                </Link>
                                <PrimaryButton @click="deleteItem(item)"
                                    >Delete</PrimaryButton
                                >
                            </td>
                        </tr>
                    </table>
                </div>

                <div class="flex justify-between mt-5 px-5">
                    <Link
                        class="text-white"
                        v-if="employees.prev_page_url"
                        :href="employees.prev_page_url"
                        >&lt;&lt; Previous</Link
                    >
                    <span v-else class="text-gray-500">
                        &lt;&lt; Previous
                    </span>
                    <Link
                        class="text-white"
                        v-if="employees.next_page_url"
                        :href="employees.next_page_url"
                        >Next &gt;&gt;</Link
                    >
                    <span v-else class="text-gray-500"> Next &gt;&gt; </span>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, Link } from "@inertiajs/vue3";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import { useForm } from "@inertiajs/vue3";

export default {
    components: {
        AuthenticatedLayout,
        Head,
        Link,
        PrimaryButton,
    },
    props: {
        employees: Object,
    },
    data() {
        return {
            form: useForm({}),
        };
    },
    mounted() {},
    methods: {
        deleteItem(item) {
            this.form.delete(route("employees.destroy", item.id), {
                preserveScroll: true,
                onSuccess: () => {},
                onError: () => {},
                onFinish: () => {},
            });
        },
    },
};
</script>
