<template>
  <div>
    <h2 mb="4">Grid Data</h2>

    <!-- Date Picker -->
    <FromToDatePicker />

    <hr class="my-4" />

    <!-- DataTable -->
    <div id="Records">
      <v-row justify="center" align="center">
        <v-col class="text-center">
          <v-card-title>
            Records
            <v-spacer></v-spacer>
            <v-text-field
              @change="getDataFromApi"
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            dense
            @sort="getDataFromApi"
            :headers="headers"
            :items="desserts"
            :sort-by="['name']"
            :sort-desc="[false, true]"
            multi-sort
            :items-per-page="5"
            :options.sync="options"
            :server-items-length="totalDesserts"
            :loading="loading"
            class="elevation-1"
          ></v-data-table>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
import FromToDatePicker from '~/components/FromToDatePicker.vue';
export default {
  data() {
    return {
      search: '',
      totalDesserts: 0,
      desserts: [],
      loading: true,
      options: {},
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Iron (%)', value: 'iron' },
      ],
    };
  },
  watch: {
    options: {
      handler() {
        console.debug('getDataFromApi()');
        this.getDataFromApi();
      },
      deep: true,
    },
  },
  methods: {
    getDataFromApi() {
      this.loading = true;
      this.fakeApiCall().then((data) => {
        this.desserts = data.items;
        this.totalDesserts = data.total;
        this.loading = false;
      });
    },
    /**
     * In a real application this would be a call to fetch() or axios.get()
     */
    fakeApiCall() {
      return new Promise((resolve, reject) => {
        const { sortBy, sortDesc, page, itemsPerPage } = this.options;
        let items = this.getDesserts();
        // search
        const query = this.search.trim().toLowerCase() || '';
        if (query) {
          items = items.filter((item) => {
            return Object.values(item)
              .join(',')
              .toLocaleLowerCase()
              .includes(query);
          });
        }
        const total = items.length;
        if (sortBy.length === 1 && sortDesc.length === 1) {
          items = items.sort((a, b) => {
            const sortA = a[sortBy[0]];
            const sortB = b[sortBy[0]];
            if (sortDesc[0]) {
              if (sortA < sortB) return 1;
              if (sortA > sortB) return -1;
              return 0;
            } else {
              if (sortA < sortB) return -1;
              if (sortA > sortB) return 1;
              return 0;
            }
          });
        }
        if (itemsPerPage > 0) {
          items = items.slice((page - 1) * itemsPerPage, page * itemsPerPage);
        }
        setTimeout(() => {
          resolve({
            items,
            total,
          });
        }, 300);
      });
    },
    getDesserts() {
      return [
        {
          name: 'フローズン ヨーグルト',
          calories: 159,
          fat: 6,
          carbs: 24,
          protein: 4,
          iron: '1%',
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9,
          carbs: 37,
          protein: 4.3,
          iron: '1%',
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16,
          carbs: 23,
          protein: 6,
          iron: '7%',
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: '8%',
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16,
          carbs: 49,
          protein: 3.9,
          iron: '16%',
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0,
          carbs: 94,
          protein: 0,
          iron: '0%',
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: '2%',
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: '45%',
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25,
          carbs: 51,
          protein: 4.9,
          iron: '22%',
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26,
          carbs: 65,
          protein: 7,
          iron: '6%',
        },
      ];
    },
  },
  components: { FromToDatePicker },
};
</script>
