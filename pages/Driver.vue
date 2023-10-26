<script setup>
import { ref } from "vue";
import { useRouter, useRoute } from "vue-router";

const router = useRouter();
const route = useRoute();
const lineData = reactive({
    labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
    datasets: [
        // {
        //     label: 'First Dataset',
        //     data: [65, 59, 80, 81, 56, 55, 40],
        //     fill: false,
        //     backgroundColor: '#2f4860',
        //     borderColor: '#2f4860',
        //     tension: 0.4
        // },
        {
            label: 'Earning graph',
            data: [28, 48, 40, 19, 86, 27, 90],
            fill: false,
            backgroundColor: '#00bb7e',
            borderColor: '#00bb7e',
            tension: 0.4
        }
    ]
});
const lineOptions = ref(null);
const visibleFull = ref(false);
const inProgress = ref(false)
const isComplete = ref(false);

const items = ref([
    {
        label: 'Pre-wash pictures',
        route: "/"
    },
    {
        label: 'Progress',
        route: "/seat",
    },
    {
        label: 'Post-wash pictures',
        route: "/payment",
    }
]);

const formObject = ref({});

const nextPage = (event) => {
    router.push(items.value[event.pageIndex + 1].route);
};
const prevPage = (event) => {
    router.push(items.value[event.pageIndex - 1].route);
};
const complete = () => {
    toast.add({severity:'success', summary:'Order submitted', detail: 'Dear, ' + formObject.value.firstname + ' ' + formObject.value.lastname + ' your order completed.'});
};

const isActive = (item) => {
    return item.route ? router.resolve(item.route).path === route.path : false;
};

definePageMeta({});
</script>

<template>
    <div className="grid">
        <div className="col-12">
            <div className="card">
                <div class="flex mb-2">
                    <Avatar style="background-color: #eff3f8; width: 5rem; height: 5rem;" image="https://marketplace.canva.com/EAFXS8-cvyQ/1/0/400w/canva-brown-and-light-brown%2C-circle-framed-instagram-profile-picture-SsX0UeCGP8g.jpg" size="large" shape="circle"></Avatar>
                    <h5 class="ml-3">Welcome back, Shariff</h5>
                </div>

                <div class="grid">
                    <div class="col-12 lg:col-6 xl:col-4">
                        <div class="card mb-0">
                            <div class="flex justify-content-between mb-3">
                                <div>
                                    <span class="block text-500 font-medium mb-3">Your Jobs</span>
                                    <div class="text-900 font-medium text-xl">12</div>
                                </div>
                                <div class="flex align-items-center justify-content-center bg-blue-100 border-round" style="width: 2.5rem; height: 2.5rem">
                                    <i class="pi pi-shopping-cart text-blue-500 text-xl"></i>
                                </div>
                            </div>
                            <span class="text-green-500 font-medium">1 new </span>
                        </div>
                    </div>
                    <div class="col-12 lg:col-6 xl:col-4">
                        <div class="card mb-0">
                            <div class="flex justify-content-between mb-3">
                                <div>
                                    <span class="block text-500 font-medium mb-3">Revenue</span>
                                    <div class="text-900 font-medium text-xl">14,422.100 Kr.</div>
                                </div>
                                <div class="flex align-items-center justify-content-center bg-orange-100 border-round" style="width: 2.5rem; height: 2.5rem">
                                    <i class="pi pi-map-marker text-orange-500 text-xl"></i>
                                </div>
                            </div>
                            <span class="text-green-500 font-medium">%52+ </span>
                            <span class="text-500">since last week</span>
                        </div>
                    </div>
                    <div class="col-12 lg:col-6 xl:col-4">
                        <div class="card mb-0">
                            <div class="flex justify-content-between mb-3">
                                <div>
                                    <span class="block text-500 font-medium mb-3">Hours</span>
                                    <div class="text-900 font-medium text-xl">540</div>
                                </div>
                                <div class="flex align-items-center justify-content-center bg-purple-100 border-round" style="width: 2.5rem; height: 2.5rem">
                                    <i class="pi pi-comment text-purple-500 text-xl"></i>
                                </div>
                            </div>
                            <span class="text-green-500 font-medium">+85 </span>
                        </div>
                    </div>

                    <div class="col-12 xl:col-6">
                        <div class="card">
                            <div class="flex justify-content-between align-items-center mb-5">
                                <h5>Jobs</h5>
                                <!-- <small>All available jobs appear at the top</small> -->
                                <div>
                                    <Button icon="pi pi-ellipsis-v" class="p-button-text p-button-plain p-button-rounded" @click="$refs.menu2.toggle($event)"></Button>
                                    <Menu ref="menu2" :popup="true" :model="items"></Menu>
                                </div>
                            </div>
                            <ul class="list-none p-0 m-0">
                                <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
                                    <div>
                                        <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Kia Rio 5 door</span>
                                        <div class="mt-1 text-600">Vejlevej 3, Aarhus C</div>
                                        <Tag class="mt-1 mr-2" severity="success" value="available"></Tag>
                                    </div>
                                    <div class="mt-2 md:mt-0 flex align-items-center">
                                        <Button label="Start" type="button" class="p-button-success" @click="visibleFull = true"></Button>
                                    </div>
                                </li>
                                <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
                                    <div>
                                        <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Alfa Romeo Giulia</span>
                                        <div class="mt-1 text-600">Akanvej 5, Skanderborg</div>
                                        <Tag class="mt-1 mr-2" severity="success" value="available"></Tag>
                                    </div>
                                    <div class="mt-2 md:mt-0 flex align-items-center">
                                        <Button label="Start" type="button" class="p-button-success" @click="visibleFull = true"></Button>
                                    </div>
                                </li>
                                <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
                                    <div>
                                        <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Bmw 1 serie</span>
                                        <div class="mt-1 text-600">Vestergade 9, Vejle C</div>
                                        <Tag class="mt-1 mr-2" severity="warning" value="in progress"></Tag>
                                    </div>
                                    <div class="mt-2 md:mt-0 flex align-items-center">
                                        <Button label="Details" type="button" :disabled="true" class="p-button-secondary"></Button>
                                    </div>
                                </li>
                                <li class="flex flex-column md:flex-row md:align-items-center md:justify-content-between mb-4">
                                    <div>
                                        <span class="text-900 font-medium mr-2 mb-1 md:mb-0">Toyota Yaris Hybrid</span>
                                        <div class="mt-1 text-600">Vinkelvej 123, Tilst</div>
                                        <Tag class="mt-1 mr-2" severity="secondary" value="completed"></Tag>
                                    </div>
                                    <div class="mt-2 md:mt-0 flex align-items-center">
                                        <Button label="Details" type="button" class="p-button-secondary"></Button>
                                    </div>
                                </li>
                            </ul>
                        </div>
                    </div>

                    <div class="col-12 xl:col-6">
                        <div class="card">
                            <h5>Earnings Overview</h5>
                            <Chart type="line" :data="lineData" :options="lineOptions" />
                        </div>
                        <!-- <div class="card">
                            <div class="flex align-items-center justify-content-between mb-4">
                                <h5>Notifications</h5>
                                <div>
                                    <Button icon="pi pi-ellipsis-v" class="p-button-text p-button-plain p-button-rounded" @click="$refs.menu1.toggle($event)"></Button>
                                    <Menu ref="menu1" :popup="true" :model="items"></Menu>
                                </div>
                            </div>

                            <span class="block text-600 font-medium mb-3">TODAY</span>
                            <ul class="p-0 mx-0 mt-0 mb-4 list-none">
                                <li class="flex align-items-center py-2 border-bottom-1 surface-border">
                                    <div class="w-3rem h-3rem flex align-items-center justify-content-center bg-blue-100 border-circle mr-3 flex-shrink-0">
                                        <i class="pi pi-dollar text-xl text-blue-500"></i>
                                    </div>
                                    <span class="text-900 line-height-3"
                                        >Richard Jones
                                        <span class="text-700">has purchased a blue t-shirt for <span class="text-blue-500">79$</span></span>
                                    </span>
                                </li>
                                <li class="flex align-items-center py-2">
                                    <div class="w-3rem h-3rem flex align-items-center justify-content-center bg-orange-100 border-circle mr-3 flex-shrink-0">
                                        <i class="pi pi-download text-xl text-orange-500"></i>
                                    </div>
                                    <span class="text-700 line-height-3">Your request for withdrawal of <span class="text-blue-500 font-medium">2500$</span> has been initiated.</span>
                                </li>
                            </ul>

                            <span class="block text-600 font-medium mb-3">YESTERDAY</span>
                            <ul class="p-0 m-0 list-none">
                                <li class="flex align-items-center py-2 border-bottom-1 surface-border">
                                    <div class="w-3rem h-3rem flex align-items-center justify-content-center bg-blue-100 border-circle mr-3 flex-shrink-0">
                                        <i class="pi pi-dollar text-xl text-blue-500"></i>
                                    </div>
                                    <span class="text-900 line-height-3"
                                        >Keyser Wick
                                        <span class="text-700">has purchased a black jacket for <span class="text-blue-500">59$</span></span>
                                    </span>
                                </li>
                                <li class="flex align-items-center py-2 border-bottom-1 surface-border">
                                    <div class="w-3rem h-3rem flex align-items-center justify-content-center bg-pink-100 border-circle mr-3 flex-shrink-0">
                                        <i class="pi pi-question text-xl text-pink-500"></i>
                                    </div>
                                    <span class="text-900 line-height-3"
                                        >Jane Davis
                                        <span class="text-700">has posted a new questions about your product.</span>
                                    </span>
                                </li>
                            </ul>
                        </div> -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <Sidebar v-model:visible="visibleFull" :baseZIndex="1000" position="full">
        <div class="card">
                <Steps :model="items" aria-label="Form Steps"
                :pt="{
                        menuitem: ({ context }) => ({
                        class: isActive(context.item) && 'p-highlight p-steps-current'
                        })
                }">
                <template #item="{ label, item, index, props }">
                        <router-link v-if="item.route" v-slot="routerProps" :to="item.route" custom>
                        <a :href="routerProps.href" v-bind="props.action" @click="($event) => routerProps.navigate($event)" @keydown.enter="($event) => routerProps.navigate($event)">
                                <span v-bind="props.step">{{ index + 1 }}</span>
                                <span v-bind="props.label">{{ label }}</span>
                        </a>
                        </router-link>
                        <span v-else v-bind="props.action">
                        <span v-bind="props.step">{{ index + 1 }}</span>
                        <span v-bind="props.label">{{ label }}</span>
                        </span>
                </template>
                </Steps>
        </div>

        <div v-if="!inProgress" class="card">
                <div class="mb-4">
                    <h5>Upload 6 pre-wash pictures (Kia Rio 5 dør)</h5>
                    <small class="mb-2">kl: 12.15</small>
                </div>
                
                <FileUpload name="demo[]" url="./upload.php" @upload="onAdvancedUpload($event)" :multiple="true" accept="image/*" :maxFileSize="1000000">
                        <template #empty>
                                <p>Drag and drop files to here to upload.</p>
                        </template>
                </FileUpload>
                <div class="flex justify-content-center mt-5">
                        <Button label="Start Job" class="p-button-raised mr-2 mb-2"  @click="inProgress = true" />
                </div>
        </div>

        <div class="card in-progress" v-if="inProgress && !isComplete">
                <div>
                        <h1>Job in progress ...</h1>
                        <div>
                            <small>Started at: kl. 12:25</small>
                        </div>
                        <Button label="Finish job" class="p-button-raised mr-2 mb-2 mt-3" @click="isComplete = true"  />
                </div>
        </div>

        <div v-if="isComplete" class="card complete">
                <h5>Upload 6 post-wash pictures</h5>
                <FileUpload name="demo[]" url="./upload.php" @upload="onAdvancedUpload($event)" :multiple="true" accept="image/*" :maxFileSize="1000000">
                        <template #empty>
                                <p>Drag and drop files to here to upload.</p>
                        </template>
                </FileUpload>
                <div class="flex justify-content-center mt-5">
                        <Button label="Finish Job" class="p-button-raised mr-2 mb-2" @click="visibleFull = false" />
                </div>
        </div>
    </Sidebar>
</template>

<style lang="scss" scoped>
.in-progress {
        text-align: center;
}
</style>
