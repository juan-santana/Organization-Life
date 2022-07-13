<template>

    <div class="grid-container">
        <div class="item2">
            <div class="firstculum">
                <img id="img" src="../assets/bici.jpg">
            </div>
        </div>
        <div class="item3">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Monday </h3>
                </div>
                <img class="plus" v-on:click="addTask()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tarea" @keyup.enter="addTask()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Lista" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartarea(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
            
        </div>
        <div class="item4">
                <div class="monday">
                    <h3> Tuesday </h3>
                </div>
                <img class="plus" v-on:click="addTaskMartes()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareamartes" @keyup.enter="addTaskMartes()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Martes" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartareamartes(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        <div class="item5">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Wednesday </h3>
                </div>
                <img class="plus" v-on:click="addTaskMiercoles()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareamiercoles" @keyup.enter="addTaskMiercoles()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Miercoles" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartareamiercoles(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        </div>
        <div class="item6">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Thursday </h3>
                </div>
                <img class="plus" v-on:click="addTaskJueves()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareajueves" @keyup.enter="addTaskJueves()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Jueves" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartarajueves(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        </div>
        <div class="item7">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Friday </h3>
                </div>
                <img class="plus" v-on:click="addTaskviernes()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareaviernes" @keyup.enter="addTaskviernes()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Viernes" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartaraviernes(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        </div>
        <div class="item8">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Saturday </h3>
                </div>
                <img class="plus" v-on:click="addTaskSabado()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareasabado" @keyup.enter="addTaskSabado()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Sabado" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartarasabado(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        </div>
        <div class="item9">
            <div class="secondcolum1">
                <div class="monday">
                    <h3> Sunday </h3>
                </div>
                <img class="plus" v-on:click="addTaskDomingo()" src="../assets/IcSharpPlus.svg">
                <input class="tarea" v-model="tareadomingo" @keyup.enter="addTaskDomingo()" type="text"
                    placeholder="Crea una tarea" />


                <div class="contneido">

                    <div>
                        <div v-for="List in Domingo" :key="List.id">
                            <input class="check" type="checkbox" @click="borrartaradomingo(List.id)">
                            <span>{{ List.title }}</span>
                        </div>

                    </div>
                </div>
            </div>
        </div>


        

    </div>
    <footer>
        <hr />
        <div>
            <span>
                <img src="../assets/copyright.png" alt="">
                 all right reversed JGSantana
            </span>
        </div>
        </footer>
</template>



<script>
import axios from 'axios'
const baseurlList = "https://json-server-life-organization.herokuapp.com/LunesWeek"
const baseurlMartes = "https://json-server-life-organization.herokuapp.com/MartesWeek"
const baseurlMiercoles = "https://json-server-life-organization.herokuapp.com/MiercolesWeek"
const baseurlJueves = "https://json-server-life-organization.herokuapp.com/JuevesWeek"
const baseurlViernes = "https://json-server-life-organization.herokuapp.com/ViernesWeek"
const baseurlSabado = "https://json-server-life-organization.herokuapp.com/SabadoWeek"
const baseurlDomingo = "https://json-server-life-organization.herokuapp.com/DomingoWeek"

export default {
    name: "MondayComponent",
    data: () => ({
        Lista: [],
        Martes: [],
        Miercoles: [],
        Jueves: [],
        Viernes: [],
        Sabado: [],
        Domingo: [],
        tarea: '',
        tareamartes: '' ,
        tareamiercoles: '',
        tareajueves: '',
        tareaviernes: '',
        tareasabado: '',
        tareadomingo: ''

    }),
    methods: {
        async obtenerdatos() {
            const res = await axios.get(baseurlList)
            const res1 = await axios.get(baseurlMartes)
            const res2 = await axios.get(baseurlMiercoles)
            const res3= await axios.get(baseurlJueves)
            const res4 = await axios.get(baseurlViernes)
            const res5 = await axios.get(baseurlSabado)
            const res6 = await axios.get(baseurlDomingo)

            this.Lista = res.data
            this.Martes = res1.data
            this.Miercoles = res2.data
            this.Jueves = res3.data
            this.Viernes = res4.data
            this.Sabado = res5.data
            this.Domingo = res6.data


        },
        async addTask() {
            if (this.tarea.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tarea.length != 0) {
                const res = await axios.post(baseurlList, { title: this.tarea });
                this.Lista = [...this.Lista, res.data];
                this.tarea = '';
            }
        },
         async addTaskMartes() {
            if (this.tareamartes.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareamartes.length != 0) {
                const res = await axios.post(baseurlMartes, { title: this.tareamartes });
                this.Martes = [...this.Martes, res.data];
                this.tareamartes = '';
            }
        },
        async addTaskMiercoles() {
            if (this.tareamiercoles.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareamiercoles.length != 0) {
                const res = await axios.post(baseurlMiercoles, { title: this.tareamiercoles });
                this.Miercoles = [...this.Miercoles, res.data];
                this.tareamiercoles = '';
            }
        },
        async addTaskJueves() {
            if (this.tareajueves.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareajueves.length != 0) {
                const res = await axios.post(baseurlJueves, { title: this.tareajueves });
                this.Jueves = [...this.Jueves, res.data];
                this.tareajueves = '';
            }
        },
        async addTaskviernes() {
            if (this.tareaviernes.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareaviernes.length != 0) {
                const res = await axios.post(baseurlViernes, { title: this.tareaviernes });
                this.Viernes = [...this.Viernes, res.data];
                this.tareaviernes = '';
            }
        },
        async addTaskSabado() {
            if (this.tareasabado.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareasabado.length != 0) {
                const res = await axios.post(baseurlSabado, { title: this.tareasabado });
                this.Sabado = [...this.Sabado, res.data];
                this.tareasabado = '';
            }
        },
        async addTaskDomingo() {
            if (this.tareadomingo.length === 0) {
                return alert("Debes llenar el input")
            }
            else if (this.tareadomingo.length != 0) {
                const res = await axios.post(baseurlDomingo, { title: this.tareadomingo });
                this.Domingo = [...this.Domingo, res.data];
                this.tareadomingo = '';
            }
        },
        async borrartarea(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/LunesWeek/" + index)
            this.obtenerdatos()
        },
        async borrartareamartes(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/MartesWeek/" + index)
            this.obtenerdatos()
        }
        ,
        async borrartareamiercoles(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/MiercolesWeek/" + index)
            this.obtenerdatos()
        }
        ,
        async borrartarajueves(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/JuevesWeek/" + index)
            this.obtenerdatos()
        }
        ,
        async borrartaraviernes(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/ViernesWeek/" + index)
            this.obtenerdatos()
        }
        ,
        async borrartarasabado(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/SabadoWeek/" + index)
            this.obtenerdatos()
        }
        ,
        async borrartaradomingo(index) {
            await axios.delete("https://json-server-life-organization.herokuapp.com/DomingoWeek/" + index)
            this.obtenerdatos()
        }
    },
    created() {
        this.obtenerdatos()
    }
}

</script>

<style>
@import "../assets/css/daysestile.css";
@import "../assets/css/bodyestile.css";
</style>