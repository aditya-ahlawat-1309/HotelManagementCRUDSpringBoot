<template>
  <div>
    <br />
    <br />

   
      <div class="q-pa-md q-gutter-sm">
        <q-btn label="Add Rooms" color="primary" @click="inception = true" />

        <q-dialog v-model="inception">
          <q-card>
            <q-card-section>
              <div class="text-h6">Room Form</div>
            </q-card-section>

            <q-card-section class="q-pt-none">
              <form>
                <label>Hotel Name</label>
                <br />
                <br/>
                <input
                  placeholder="&nbsp;&nbsp; Enter Hotel Name"
                  v-model="form.hotelName"
                  required
                  style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"

                />
                <br />
                <br />
                <label>Room No.</label>
                <br />
                <br/>
                <input
                  placeholder="&nbsp;&nbsp; Enter Room Number"
                  v-model="form.number"
                  required
                  style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"

                />

                <br />
                <br />

                <label>Room Type</label>
                <br />
                <br/>
                <input
                  placeholder="&nbsp;&nbsp; Enter Room Type"
                  v-model="form.type"
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

                <label>Available</label>
                <br />
                <br/>
                <input
                  placeholder="&nbsp;&nbsp; Enter Availability"
                  v-model="form.available"
                  required
                  style="margin-top:-10%;border:none; height:50px;width:350px;background-color:#f3f3e3;border-radius:20px;color:black"

                />

                <br />
                <br />

                <q-btn
                  @click="postRoom()"
                  style="background: #ff0080; color: white"
                  label="Add Room"
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
          title="ROOM 's Intel"
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
    label: "R O O M 'S",
    align: "left",
    field: (row) => row.hotelName,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "number",
    align: "center",
    label: "Room No.",
    field: "number",
    sortable: true,
  },
  { name: "type", label: "Room Type", field: "type", sortable: true },
  {
    name: "price",
    align: "center",
    label: "basePrice",
    field: "basePrice",
    sortable: true,
  },
  { name: "available", label: "Available", field: "available", sortable: true },
];

const rows = [
  {
    name: "Taj Hotel",
    number: "101",
    type: "Suite",
    price: "$957",
    available: "Yes",
  },
  {
    name: "Taj Hotel",
    number: "789",
    type: "Deluxe",
    price: "$757",
    available: "Yes",
  },
  {
    name: "W",
    number: "1546",
    type: "King",
    price: "$557",
    available: "Yes",
  },

  //   {
  //     name:  {{ backend.data ? backend.data[backend.data.length - 1].hotelName : "" }},
  //     number:  {{ backend.data ? backend.data[backend.data.length - 1].number : "" }},
  //     type:  {{ backend.data ? backend.data[backend.data.length - 1].type : "" }},
  //     price:  {{ backend.data ? backend.data[backend.data.length - 1].basePrice : "" }},
  //     available:  {{ backend.data ? backend.data[backend.data.length - 1].available : "" }},
  //   }
];

export default defineComponent({
  name: "HotelsPage",
  setup() {
    const backend = ref([]);

    function getRoom() {
      axios
        .get("https://hotel-management-crud.herokuapp.com/api/getRoom")
        .then((response) => {
          backend.value = response.data;
          console.log(response.data);
        })
        .catch((err) => {
          console.error(err);
        });
    }

    getRoom();

    return {
      columns,
      rows,
      inception: ref(false),
      secondDialog: ref(false),
      form: {
        hotelName: "",
        number: "",
        type: "",
        basePrice: "",
        available: "",
      },
      backend
    };
  },
  methods: {
    postRoom() {
      axios
        .post("https://hotel-management-crud.herokuapp.com/api/postRoom", this.form)
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
