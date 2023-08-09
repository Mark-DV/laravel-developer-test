<template>
    <AuthenticatedLayout>
        <!-- Title -->
        <Head title="Companies" />

        <template #header>
            <h2
                class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight"
            >
                Companies
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="flex justify-end mb-6">
                    <Link :href="route('companies.create')">
                        <PrimaryButton>Create Company</PrimaryButton>
                    </Link>
                </div>
                <div
                    class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg pb-2"
                >
                    <table class="w-full">
                        <tr>
                            <th class="text-white p-4 text-left">No</th>
                            <th class="text-white p-4 text-left">
                                Company Name
                            </th>
                            <th class="text-white p-4 text-left">
                                Company Email
                            </th>
                            <th class="text-white p-4">Logo</th>
                            <th class="text-white p-4">Actions</th>
                        </tr>
                        <tr
                            v-for="(company, index) in companies.data"
                            :key="company.id"
                        >
                            <td class="text-white px-4 py-2">
                                {{
                                    index +
                                    1 +
                                    (companies.current_page - 1) * 10
                                }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ company.name }}
                            </td>
                            <td class="text-white px-4 py-2">
                                {{ company.email }}
                            </td>
                            <td class="text-white px-4 py-2 text-center">
                                <img
                                    v-if="company.logo"
                                    :src="company.logo"
                                    alt="Company Logo"
                                    width="50"
                                    height="50"
                                    class="m-auto"
                                />
                            </td>
                            <td
                                class="text-white px-8 py-2 space-x-4 text-center whitespace-nowrap w-1"
                            >
                                <Link
                                    :href="route('companies.show', company.id)"
                                >
                                    <PrimaryButton>Show</PrimaryButton>
                                </Link>
                                <Link
                                    :href="route('companies.edit', company.id)"
                                >
                                    <PrimaryButton>Edit</PrimaryButton>
                                </Link>
                                <PrimaryButton @click="deleteCompany(company)"
                                    >Delete</PrimaryButton
                                >
                            </td>
                        </tr>
                    </table>
                </div>

                <div class="flex justify-between mt-5 px-5">
                    <Link
                        class="text-white"
                        v-if="companies.prev_page_url"
                        :href="companies.prev_page_url"
                        >&lt;&lt; Previous</Link
                    >
                    <span v-else class="text-gray-500">
                        &lt;&lt; Previous
                    </span>
                    <Link
                        class="text-white"
                        v-if="companies.next_page_url"
                        :href="companies.next_page_url"
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
        companies: Object,
    },
    data() {
        return {
            form: useForm({}),
        };
    },
    computed() {},
    created() {},
    mounted() {},
    methods: {
        deleteCompany(item) {
            this.form.delete(route("companies.destroy", item.id), {
                preserveScroll: true,
                onSuccess: () => {},
                onError: () => {},
                onFinish: () => {},
            });
        },
    },
};
</script>
