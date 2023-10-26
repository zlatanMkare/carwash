<script setup>
import { ProductService } from '@/service/ProductService';
const products = ref(null);

onMounted(() => {
    ProductService.getProductsSmall().then((data) => (products.value = data));
});

const formatCurrency = (value) => {
    return value.toLocaleString('da-DK', { style: 'currency', currency: 'DKK' });
};
</script>

<template>
    <div className="grid">
        <div className="col-12">
            <div className="card">
                <h5>All Jobs</h5>
                <p>Use this page to start from scratch and place your custom content.</p>

                <DataTable :value="products" :rows="10" :paginator="true" responsiveLayout="scroll">
                    <!-- <Column style="width: 15%">
                        <template #header> Image </template>
                        <template #body="slotProps">
                            <img :src="slotProps.data.carImage" :alt="slotProps.data.carType" width="50" class="shadow-2" />
                        </template>
                    </Column> -->
                    <Column field="carType" header="Car Type" style="width: 25%"></Column>
                    <Column field="owner" header="Job by" style="width: 25%"></Column>
                    <Column field="price" header="Price" :sortable="true" style="width: 15%">
                        <template #body="slotProps">
                            {{ formatCurrency(slotProps.data.price) }}
                        </template>
                    </Column>
                    <Column field="location" header="Location" style="width: 25%">
                        <template #body="slotProps">
                            {{ slotProps.data.location }}
                        </template>
                    </Column>
                    <Column field="status" header="Status" style="width: 15%">
                        <template #body="slotProps">
                            <Tag v-if="slotProps.data.status === 'in progress'" class="mr-2" severity="info" :value="slotProps.data.status"></Tag>
                            <Tag v-if="slotProps.data.status === 'Finished'" class="mr-2" severity="success" :value="slotProps.data.status"></Tag>
                            <Tag v-if="slotProps.data.status === 'Not started'" class="mr-2" severity="warning" :value="slotProps.data.status"></Tag>

                        </template>
                    </Column>
                    <Column style="width: 15%">
                        <template #header> Assign Job </template>
                        <template #body="slotProps">
                            <Button label="Assign" type="button" @click="visibleFull = true" :disabled="slotProps.data.status !== 'Not started'"></Button>
                        </template>
                    </Column>
                </DataTable>
            </div>
        </div>
    </div>
</template>
