<template>
	<div class="grid grid-cols-12 m-5 gap-5" v-if="isLoading">
		<Skeleton height="50vh" width="100%" class="col-span-12"></Skeleton>
	</div>
	<div class="grid grid-cols-12 m-5 gap-5 mb-24 lg:mb-5" v-else>
		<Card class="col-span-12 xl:col-span-8 shadow-md">
			<template #title>
				<div class="flex justify-between">
                    <h3>
						Data Payroll Pegawai
					</h3>
                    <div class="flex gap-2">
                        <RouterLink to="/payroll/tambah">    
                            <Button icon="pi pi-plus-circle" label="Tambah Payroll"></Button>
                        </RouterLink>
                        <Button icon="pi pi-external-link" label="Export" @click="exportCSV($event)" />
                    </div>
                </div>
			</template>
			<template #content>
				<DataTable :value="dataPayroll"></DataTable>
			</template>
		</Card>
		<Card class="col-span-12 xl:col-span-4 shadow-md">
			<template #title>
				Total Payroll Bulan Ini
			</template>
			<template #content>
				
			</template>
		</Card>
	</div>
</template>

<script>
export default {
	name:'Payroll',
	inject:['default'],
	data() {
		return {
			isLoading: false,
			dataPayroll: []
		}
	},
	methods: {
		async getPayroll() {
			await axios.get('payroll', {
				headers: {
					'Authorization': `Bearer ${this.default.token}`
				}
			}).then((res) => {
				console.log(res)
			})
		}
	},
	mounted() {
		this.getPayroll()
	},
}
</script>