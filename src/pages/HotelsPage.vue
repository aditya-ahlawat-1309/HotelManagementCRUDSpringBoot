<template>
  <div>
    <br />
    <br />

    <div class="q-pa-md q-gutter-sm">
      <q-btn label="Add Hotels" color="primary" @click="inception = true" />

      <q-dialog v-model="inception">
        <q-card>
          <q-card-section>
            <div class="text-h6">Hotel Form</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <form>
              <label>Hotel Name</label>
              <br />
              <br/>
              <input
                placeholder="&nbsp;&nbsp;Enter Hotel Name"
                v-model="form.hotelName"
                required
                style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"
              />
              <br />
              <br />
              <label>Address</label>
              <br />
              <br/>
              <input
                placeholder="&nbsp;&nbsp; Enter Address Name"
                v-model="form.address"
                required
                style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"

              />

              <br />
              <br />

              <label>Base Price</label>
              <br />
              <br/>
              <input
                placeholder="&nbsp;&nbsp; Enter Base Price"
                v-model="form.basePrice"
                required
                style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"

              />

              <br />
              <br />

              <q-btn
                @click="postHotel()"
                style="background: #ff0080; color: white"
                label="Add Hotel"
              />
            </form>
          </q-card-section>

          <q-card-actions align="right" class="text-primary">
            <q-btn flat label="Close" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-dialog
        v-model="secondDialog"
        persistent
        transition-show="scale"
        transition-hide="scale"
      >
        <q-card class="bg-teal text-white" style="width: 300px">
          <q-card-section>
            <div class="text-h6">Persistent</div>
          </q-card-section>

          <q-card-actions align="right" class="bg-white text-teal">
            <q-btn flat label="OK" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>
    </div>

    <div class="q-pa-md">
      <br />
      <br />

      <q-table
        title="HOTEL 's Intel"
        :rows="backend"
        :columns="columns"
        row-key="name"
      />
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";
import axios from "axios";
const columns = [
  {
    name: "name",
    required: true,
    label: "H O T E L 'S",
    align: "left",
    field: (row) => row.hotelName,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "address",
    align: "center",
    label: "Address",
    field: "address",
    sortable: true,
  },
  { name: "base", label: "Base Price", field: "basePrice", sortable: true },
];

const rows = [
  {
    name: "Taj Hotel",
    address: "Banjara Hills, Hyd",
    basePrice: "$557",
  },
  {
    name: "W",
    address: "Jubilee Hills, Hyd",
    basePrice: "$359",
  },

  //   {
  //     name:  {{ backend.data ? backend.data[backend.data.length - 1].hotelName : "" }},
  //     address:  {{ backend.data ? backend.data[backend.data.length - 1].address : "" }},
  //     base:  {{ backend.data ? backend.data[backend.data.length - 1].basePrice : "" }},
  //   }
];

export default defineComponent({
  name: "HotelsPage",
  setup() {
    const backend = ref([]);

    function getHotel() {
      axios
        .get("http://localhost:5000/api/getHotel")
        .then((response) => {
          backend.value = response.data;
          console.log(response.data);
        })
        .catch((err) => {
          console.error(err);
        });
    }

    getHotel();

    return {
      columns,
      rows,
      inception: ref(false),
      secondDialog: ref(false),
      form: {
        hotelName: "",
        address: "",
        basePrice: "",
      },
      backend,
    };
  },

  methods: {
    postHotel() {
      axios
        .post("http://localhost:5000/api/postHotel", this.form)
        .then((response) => {
          console.log(response);
          window.location.reload();
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
});
</script>
