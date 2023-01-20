<template>
  <div id="app-container">
    <DxDataGrid :data-source="state.data">
      <DxColumn data-field="0" caption="병원코드" />
      <DxColumn data-field="1" caption="유저ID" />
      <DxColumn data-field="2" caption="유저이름" />
    </DxDataGrid>
    <DxCalendar> </DxCalendar>
  </div>
</template>

<script>
import 'devextreme/dist/css/dx.light.css';
import DxDataGrid, { DxColumn } from 'devextreme-vue/data-grid';
import { DxCalendar } from 'devextreme-vue/calendar';

import { reactive } from 'vue';
import axios from 'axios';

export default {
  components: {
    DxDataGrid,
    DxColumn,
    DxCalendar,
  },
  setup() {
    const state = reactive({
      data: [],
    });

    axios
      .get('/api/memos')
      .then((res) => {
        state.data = res.data;
      })
      .catch((err) => {
        console.log(err.response);
      });

    return { state };
  },
};
</script>

<style>
#dataGrid {
  height: 500px;
}
</style>
