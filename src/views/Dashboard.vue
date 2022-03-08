<template>
  <div>
    <Header />

    <div class="container izquierda pt-5">
     <table id="example" class="table table-striped" style="width:100%">
        <thead>
            <tr>
                <th>Paciente</th>
                <th>Direccion</th>
                <th>Barrio</th>
                <th>Telefono</th>
                <th>Orden de trabajo</th>
                <th>Orden de servicio</th>
                <th>Servicio</th>
                <th>Valido Hasta</th>
                <th>Asig.</th>
                <th>Real.</th>
                <th>Obs.</th>
                <th></th>
                <th>Firmas</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(lista, i) in this.rowData" :key="i">
                <td ><img src="@/assets/user.jpg" style="width:75px" id="icon" alt="User Icon" /></td>
                <td>{{lista.paciente.primer_nombre}} {{lista.paciente.primer_apellido}}</td>
                <td>{{lista.paciente.direccion}}</td>
                <td>{{lista.paciente.barrio}}</td>
                <td>{{lista.paciente.telefono}}</td>
                <td>{{lista.ordentrabajo_id}}</td>
                <td>{{lista.ordenservicio_id}}</td>
                <td>{{lista.servicio}}</td>
                <td>{{lista.ordentrabajo_validahasta}}</td>
                <td>{{lista.actividades_asignadas}}</td>
                <td>{{lista.actividades_realizadas}}</td>
                <td>{{lista.observacion || ""}}</td>
                <td></td>
                <td>{{lista.firma || ""}}</td>
            </tr>
        </tbody>
    </table>
    </div>

    <Footer />
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import axios from "axios";
export default {
  name: "Dashboard",
  data() {
    return {  
      rowData: [],
    };
  },
  components: {
    Header,
  },
  mounted(){
      this.agenda();
  },
  methods: {
    agenda() {
      let data = {
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
          Authorization: "Bearer " + localStorage.getItem("access_token"),
        },
      };
      axios
        .get("http://159.223.115.64:8000/api/v1/AgendaDomiciliaria", data)
        .then((data) => {
          this.rowData = data.data;
        });
    },
  },
};
</script>
<style scoped>
.izquierda {
  text-align: left;
}
</style>
