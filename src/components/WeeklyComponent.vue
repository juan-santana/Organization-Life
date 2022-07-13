<template>
   

    <!--Body-->
    <div class="conteinerweekly">

        <div class="contenidobody">
            <!-- aqui estan las tabs -->
            <div class="tabs">
                <div class="nav-tabs">
                    <div class="nav-item" @click="setActive('tab-1')">
                        <img src="../assets/table.svg" />
                        <span>List</span>
                    </div>
                    <div class="nav-item" @click="setActive('tab-2')">
                        <img src="../assets/card-checklist.svg" />
                        Shopping list
                    </div>
                </div>
                <div class="todo">
                    <img src="../assets/clock.svg">
                    <h2>TO DO</h2>
                </div>
            </div>
            <div class="tab-content1">
                <div class="tab-pane1" v-show="isActive('tab-1')">
                    <div class="forexample">

                        <table class="table table-bordered">
                            <thead>
                                <tr class="bordecolumnas">
                                    <th scope="col">Task</th>

                                    <th scope="col">Status</th>
                                    <th scope="col"><span class="fa fa-pen"></span></th>

                                    <th scope="col"><span class="fa fa-trash"></span></th>
                                </tr>
                            </thead>
                            <tbody v-for="Tarea in Tareas" :key="Tarea.id">
                                <tr>
                                    <th>{{ Tarea.title }}</th>

                                    <td>To-DO</td>
                                    <td v-on:click="ViewSHowInput(Tarea.id, Tarea.title)" class="iconosocultos">
                                        <div>
                                            <span class="fa fa-pen colorfa1"></span>
                                        </div>
                                    </td>

                                    <td @click="deletTask(Tarea.id)" class="iconosocultos">
                                        <div>
                                            <span class="fa fa-trash colorfa"></span>
                                        </div>
                                    </td>

                                </tr>
                            </tbody>
                            <tfoot>
                                <tr>
                                    <div class="addtask">

                                        <input v-model="tarea" @keyup.enter="addDataTask()" type="text"
                                            placeholder="Crea una tarea" />
                                        <div>
                                            <div v-if="display">
                                                <img v-on:click="addDataTask()" src="../assets/IcSharpPlus.svg">
                                            </div>
                                            <div v-else v-on:click="editDataTask(this.indexValue)">
                                                <span class="fa fa-pen colorfa1"></span>
                                            </div>
                                        </div>
                                        <div class="cout">
                                            Count : {{ Tareas.length }}
                                        </div>


                                    </div>
                                </tr>
                            </tfoot>
                        </table>
                    </div>

                </div>
                <div class="tab-pane1" v-show="isActive('tab-2')">
                    <div class="forexample">

                        <table class="table table-bordered">
                            <thead>
                                <tr class="bordecolumnas">
                                    <th scope="col">Task</th>

                                    <th scope="col">Status</th>
                                    <th scope="col"><span class="fa fa-pen"></span></th>

                                    <th scope="col"><span class="fa fa-trash"></span></th>
                                </tr>
                            </thead>
                            <tbody v-for="Tarea in shoppingList" :key="Tarea.id">
                                <tr>
                                    <th>{{ Tarea.title }}</th>
                                    <td>To-DO</td>
                                    <td v-on:click="ViewSHowInput(Tarea.id, Tarea.title)" class="iconosocultos">
                                        <div>
                                            <span class="fa fa-pen colorfa1"></span>
                                        </div>
                                    </td>

                                    <td @click="deletTaskShopping(Tarea.id)" class="iconosocultos">
                                        <div>
                                            <span class="fa fa-trash colorfa"></span>
                                        </div>
                                    </td>

                                </tr>
                            </tbody>
                            <tfoot>
                                <tr>
                                    <div class="addtask">

                                        <input v-model="tarea" @keyup.enter="addDataList()" type="text"
                                            placeholder="Crea una tarea" />
                                        <div>
                                            <div v-if="display">
                                                <img v-on:click="addDataList()" src="../assets/IcSharpPlus.svg">
                                            </div>
                                            <div v-else v-on:click="editDataTaskShopping(this.indexValue)">
                                                <span class="fa fa-pen colorfa1"></span>
                                            </div>
                                        </div>
                                        <div class="cout">
                                            Count : {{ shoppingList.length }}
                                        </div>

                                    </div>

                                </tr>

                            </tfoot>
                        </table>
                    </div>

                </div>
            </div>
        </div>

    </div>


</template>

<script>

//importando axios y creando variables constantes de la api

import axios from 'axios';

const baseurltask = "https://json-server-life-organization.herokuapp.com/task"
const baseurlShoppingList = "https://json-server-life-organization.herokuapp.com/shoppinglist"




export default {
    name: "WeeklyComponent",
    //definiendo variables a usar
    data: () => ({
        activeTab: 'tab-1',
        shoppingList: [],
        tarea: '',
        edittask: '',
        Tareas: [],
        display: true,
        indexValue: 0

    }),
    //creando los metodos
    methods: {
        // metodo para obtener datos mediante axios y asignandolo al array Tareas []
        async obtenerdatos() {
            try {
                const res = await axios.get(baseurltask);
                this.Tareas = res.data;
                const res1 = await axios.get(baseurlShoppingList);
                this.shoppingList = res1.data;
                
            } catch (error) {
                console.log(error);
            }
        },
        // metodo para agregar datos mediante axios con post y algunas validaciones
        async addDataTask() {
            if (this.tarea.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tarea.length != 0) {
                const res = await axios.post(baseurltask, { title: this.tarea });
                this.Tareas = [...this.Tareas, res.data];
                this.tarea = '';
            }
        },
        async addDataList() {
            if (this.tarea.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tarea.length != 0) {
                const res = await axios.post(baseurlShoppingList, { title: this.tarea });
                this.shoppingList = [...this.shoppingList, res.data];
                this.tarea = '';
            }
        },
        // metodo para mostrar los iconos de editar y agregar y obteniendo el indece del array seleccionado
        async ViewSHowInput(indexValue, indextitle) {

            this.indexValue = indexValue
            this.tarea = indextitle
            this.display = false
        },
        // metodo para editar el indice seleccionado por el metodo vieshowimput
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

                const res = await axios.put("https://json-server-life-organization.herokuapp.com/task/" + index, { title: this.tarea });
                this.tarea = res.data.title;
                this.display = true;
                this.tarea = ''
                this.obtenerdatos()
            }
        },
        async editDataTaskShopping(index) {
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

                const res = await axios.put("https://json-server-life-organization.herokuapp.com/shoppinglist/" + index, { title: this.tarea });
                this.tarea = res.data.title;
                this.display = true;
                this.tarea = ''
                this.obtenerdatos()
            }
        },
        // metodo para borrar el item selecionado y obtenemos nuevamente los datos del api
        async deletTask(Index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/task/" + Index)
            this.obtenerdatos()
        },
        async deletTaskShopping(Index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/shoppinglist/" + Index)
            this.obtenerdatos()
        },
        // metodo para las ventanas si seteando el tab clickeado y asignandoselo a activeTab
        setActive(tab) {
            this.activeTab = tab
        },
        // metodo para si el tab esta activo y retornamos si el active tab es igual al active tab y lo mostramos con v-show
        isActive(tab) {
            return this.activeTab === tab;
        },
        //
    },

    // metodo para que al entrar a la pagina carge el api y muestre los datos
    created() {
        this.obtenerdatos()


    }

};

</script>
<style>
@import "../assets/css/bodyestile.css";
</style>
