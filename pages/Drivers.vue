<script setup>
import { onMounted, reactive, ref, watch } from 'vue';

import { CustomerService } from '@/service/CustomerService';
const drivers = ref(null);

onMounted(() => {
    CustomerService.getCustomersSmall().then((data) => (drivers.value = data));
});

const formatCurrency = (value) => {
    return value.toLocaleString('da-DK', { style: 'currency', currency: 'DKK' });
};
</script>


<template>
    <div className="grid">
        <div className="col-12">
            <div className="card">
                <h5>All Drivers</h5>
                <p>Use this page to start from scratch and place your custom content.</p>

                <DataTable :value="drivers" :rows="15" :paginator="true" responsiveLayout="scroll">
                    <Column style="width: 15%">
                        <template #header> Image </template>
                        <template #body="slotProps">
                            <Avatar :image="slotProps.data.image" :style="{ 'background-color': '#ffffff' }" size="xlarge" shape="circle"></Avatar>
                        </template>
                    </Column>
                    <Column field="name" header="Name" style="width: 25%"></Column>
                    <Column field="distance" header="Distance(km)" :sortable="true" style="width: 15%"></Column>
                    <Column field="status" header="Status" style="width: 25%">
                        <template #body="slotProps">
                            <Tag v-if="slotProps.data.status === 'available'" class="mr-2" severity="success" :value="slotProps.data.status"></Tag>
                            <Tag v-if="slotProps.data.status === 'Not available'" class="mr-2" severity="danger" :value="slotProps.data.status"></Tag>
                        </template>
                    </Column>
                    <Column style="width: 15%">
                        <template #header> Details </template>
                        <template #body>
                            <router-link to="/driver" class="layout-topbar-logo">
                                <Button label="Details" type="button"></Button>
                            </router-link>
                        </template>
                    </Column>
                </DataTable>
            </div>
        </div>
    </div>
</template>
