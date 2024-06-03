<template>
  <div class="grid">
    <div class="card col-12 lg:col-4 col-offset-4 shadow-4 mt-4">
      <h1>Digimon</h1>
      <DataTable :value="digimons" :paginator="true" :rows="5"  tableStyle="min-width: 30rem">
        <Column field="name" header="Name"></Column>
        <Column header="Image">
          <template #body="slotProps">
            <img :src="slotProps.data.img" :alt="slotProps.data.name" class="w-6rem border-round" />
          </template>
        </Column>
        <Column field="level" header="Level"></Column>
        <template #footer>
          In totale ci sono {{ digimons ? digimons.length : 0 }} digimons.
        </template>
      </DataTable>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import { defineComponent, ref } from 'vue';
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';
import Button from 'primevue/button';

export default defineComponent({
  components: {
    DataTable,
    Column,
    Button
  },
  setup() {
    const digimons = ref([]);

    const fetchDigimons = async () => {
      try {
        const response = await axios.get('https://digimon-api.vercel.app/api/digimon');
        digimons.value = response.data;
      } catch (error) {
        console.error('Error fetching Digimons:', error);
      }
    };

    fetchDigimons();

    return { digimons, fetchDigimons };
  }
});
</script>

<style>

.card {
  background: linear-gradient(135deg, #3b3b5f, #28283d) !important;
  color: #fff !important;
  border-radius: 10px !important;
  padding: 20px !important;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2) !important;
}

.p-datatable {
  background-color: transparent !important;
  color: #fff !important;
  font-size: 0.75rem !important;
}


.p-paginator {
    background: #ffffff;
    color: #6c757d;
    border: solid #e9ecef;
    border-width: 0;
    padding: 0.5rem 1rem;
    border-radius: 0px !important ;
}

.p-datatable .p-datatable-tbody > tr {
  background-color: #4e4e7f !important ;
  border-color: #4e4e7f !important ;
  color: #fff !important;
}

.p-datatable .p-datatable-tbody > tr:nth-child(odd) > td {
  background-color: #3b3b5f !important;
}

.p-datatable .p-datatable-tbody > tr:nth-child(even) > td {
  background-color: #2c2c46 !important;
}

.p-datatable .p-datatable-tbody > tr > td {
  border-color: #4e4e7f !important ;
}

.text-xl {
  font-size: 1.25rem;
}

.image-size {
  width: 3rem;
}

.border-round {
  border-radius: 0.5rem;
}

.shadow-4 {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
</style>




