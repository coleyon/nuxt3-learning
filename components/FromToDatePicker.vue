<template>
  <!-- Date Picker -->
  <div id="datePicker" class="mb-4">
    <v-sheet color="white" elevation="1" outlined rounded justify="center">
      <v-row justify="center" align="center">
        <!-- startDate -->
        <v-col>
          <v-menu
            ref="startDateMenu"
            v-model="startDateMenu"
            :close-on-content-click="false"
            :return-value.sync="startDate"
            transition="scale-transition"
            offset-y
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="startDate"
                label="Picker in startDateMenu"
                prepend-icon="mdi-calendar"
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="startDate"
              no-title
              scrollable
              :first-day-of-week="0"
              locale="jp-ja"
              :day-format="(date) => new Date(date).getDate()"
            >
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="startDateMenu = false">
                Cancel
              </v-btn>
              <v-btn
                text
                color="primary"
                @click="$refs.startDateMenu.save(startDate)"
              >
                OK
              </v-btn>
            </v-date-picker>
          </v-menu>
        </v-col>
        <!-- endDate -->
        <v-col>
          <v-menu
            ref="endDateMenu"
            v-model="endDateMenu"
            :close-on-content-click="false"
            :return-value.sync="endDate"
            transition="scale-transition"
            offset-y
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="endDate"
                label="Picker in endDateMenu"
                prepend-icon="mdi-calendar"
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="endDate"
              no-title
              scrollable
              :first-day-of-week="0"
              locale="jp-ja"
              :day-format="(date) => new Date(date).getDate()"
            >
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="endDateMenu = false">
                Cancel
              </v-btn>
              <v-btn
                text
                color="primary"
                @click="$refs.endDateMenu.save(endDate)"
              >
                OK
              </v-btn>
            </v-date-picker>
          </v-menu>
        </v-col>

        <v-spacer></v-spacer>
      </v-row>
    </v-sheet>
  </div>
</template>

<script>
export default {
  // table datas
  data() {
    return {
      // Date picker
      startDate: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      startDateMenu: '',
      endDate: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      endDateMenu: '',
    };
  },
};
</script>
<style scoped></style>
