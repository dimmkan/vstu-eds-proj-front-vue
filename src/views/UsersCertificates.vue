<template>
    <ProgressSpinner v-if="loading" />
    <TreeTable v-if="!loading" :value="nodes" :filters="filters" filterMode="lenient" dataKey="key" tableStyle="min-width: 50rem">
        <template #header>
            <div style="text-align: center" class="text-xl font-bold">Список прикрепленных к пользователю ЭЦП</div>
            <div style="text-align: right">
            <i class="pi pi-search" style="margin: 4px 4px 0px 0px;"></i>
            <InputText v-model="filters['global']" placeholder="Глобальный поиск" size="50" />
        </div>
        </template>
        <Column field="user_name" header="Имя пользователя" expander style="width: 34%">
            <template #filter>
                <InputText v-model="filters['user_name']" type="text" placeholder="Отбор по имени пользователя" size="50"/>
            </template>
        </Column>
        <Column field="comp_name" header="Имя компьютера" style="width: 33%"></Column>
        <Column field="org_name" header="Организация" style="width: 33%"></Column>
    </TreeTable>
</template>

<script>
import LabelsService from '@/services/LabelsService.js';
import { FilterMatchMode, FilterOperator } from 'primevue/api';

export default {
  created() {
    this.labelsService = new LabelsService();
  },

  mounted() {
    this.reloadShowcase();
  },

  data() {
    return {
        nodes: null,
        loading: true,
        filters: {},
    }
  },

  methods: {
    reloadShowcase() {
      this.labelsService.getShowcaseData().then(async (data) => {
        console.log(data);
        this.nodes = data;
        this.loading = false;
      });
    },
  },
}
</script>

<style>

</style>