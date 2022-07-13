<template>
   <header>
        <hr />

    </header>
  <div class="contenidoheaderweekly">

    <div class="firstculum">
      <img class="img" src="../assets/weekly.jpg">

    </div>
    <!-- Aqui va la lista con datos que quiera el usuario -->
    <div class="secondcolum">
      <h2>Weekly</h2>
      <hr />
      <!-- aqui tenemos un array de listas que esta siendo recorrido y mostrandose -->
      <div class="div-list">
        <tfoot>
          <tr>
            <div class="addtask">

              <input v-model="tarea" @keyup.enter="addDataList()" type="text" placeholder="Crea una tarea" />
              <div>
                <div v-if="display">
                  <img v-on:click="addDataList()" src="../assets/IcSharpPlus.svg">
                </div>
                <div v-else v-on:click="editDataTask(this.indexValue)">
                  <span class="fa fa-pen colorfa1"></span>
                </div>
              </div>

            </div>
          </tr>
        </tfoot>
        <table class="table table-bordered" v-if="(this.Listas != 0)" >
          <thead>
            <tr class="bordecolumnas">
              <th scope="col" class="col-1">Done</th>
              <th scope="col" class="col-5">Task</th>
              <th scope="col"><span class="fa fa-pen"></span></th>

              <!-- <th scope="col"><span class="fa fa-trash"></span></th> -->
            </tr>
          </thead>
          <tbody v-for="Tarea in Listas" :key="Tarea.id">
            <tr>
              <td><input type="checkbox"  @click="deletTask(Tarea.id)"></td>
              <th>{{ Tarea.title }}</th>
              <td v-on:click="ViewSHowInput(Tarea.id, Tarea.title)" class="iconosocultos">
                <div>
                  <span class="fa fa-pen colorfa1"></span>
                </div>
              </td>

              <!--  <td @click="deletTaskShopping(Tarea.id)" class="iconosocultos">
                <div>
                  <span class="fa fa-trash colorfa"></span>
                </div>
              </td> -->

            </tr>
          </tbody>

        </table>

      </div>
    </div>
  </div>

</template>

<script>

import axios from 'axios'
const baseurlList = "https://json-server-life-organization.herokuapp.com/Listas"


export default {
  name: 'ListComponent',
  data: () => ({
    Listas: [],
    cheked: false,
    indexValue: 0,
    tarea: '',
    display: true
  }),
  methods: {
    async obtenerdatos() {
      try {
        const res = await axios.get(baseurlList);
        this.Listas = res.data;
      } catch (error) {
        console.log(error)
      }
    },
    async addDataList() {
      if (this.tarea.length === 0) {
        return alert("Debes llenar el input")
      }
      else if (this.tarea.length != 0) {
        const res = await axios.post(baseurlList, { title: this.tarea });
        this.Listas = [...this.Listas, res.data];
        this.tarea = '';
      }
    },
    async editDataTask(index) {
      //validacion para que si la proiedad tarea esta vacia retorne un alerta que obliga a llenar el input
      if (this.tarea.length === 0) {
        this.display = true
        return alert("Debes llenar el input")
      }
      /*  el caso contrario a que este lleno, obteniendo el indice que seleccionamos en ViewSHowInput() metodo. 
      lo pasamos al put junto a la url, asignamos el titulo de la tarea que sea igual la tarea y ocultamos el icono 
      de editar y hacemos get nuevamente a la api para mostrar los datos
      */
      else {

        const res = await axios.put("https://json-server-life-organization.herokuapp.com/Listas/" + index, { title: this.tarea });
        this.tarea = res.data.title;
        this.display = true;
        this.tarea = ''
        this.obtenerdatos()
      }

    },
    async ViewSHowInput(indexValue, indextitle) {

      this.indexValue = indexValue
      this.tarea = indextitle
      this.display = false
    },

    async deletTask(Index) {
      await axios.delete("https://json-server-life-organization.herokuapp.com/Listas/" + Index)
      
      this.obtenerdatos()
    },


  },
  // metodo para que al entrar a la pagina carge el api y muestre los datos
  created() {
    this.obtenerdatos()


  }
}
</script>
<style>
@import "../assets/css/bodyestile.css";
</style>