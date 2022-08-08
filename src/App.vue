<template>
  <h1 class="display-4 text-center">PruebaFE</h1>
    <hr>
  <center>
    Nombre: <input type="text" v-model="this.nombre"/>
    Apellido: <input type="text" v-model="this.apellido"/>
          
    <button class="btn" @click="postApi()">Guardar</button>
          
    <div class="page-container">
        <div class="container">
          <div class="row">
            <div class="column">
              <table>
                <thead>
                  <tr>
                    <th>#ID</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="todo of todos" v-bind:key="todo.id">
                    <td>{{todo.id}}</td>
                    <td>{{todo.firstName}}</td>
                    <td>{{todo.lastName}}</td>
                      <td><input type="text" v-model="todo.firstName"/></td>
                      <td><input type="text" v-model="todo.lastName"/></td>
                      <td><button v-on:click="deleteApi(todo.id)"></button></td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </center>
</template>

<script>
import axios from "axios";
const apiUrl = "https://apicsharps.azurewebsites.net/users/";

export default {
  data() {
    return {
      todos:[]
    }
  },
  methods: {
    async getApi(){
      await axios.get(apiUrl).then((resp) => {this.todos = resp.data;}).catch((err) => {console.log(err);})
    },
    async postApi(){
      await axios.post(apiUrl,{firstName:this.nombre,lastName:this.apellido}).then((resp) => {console.log(resp)});
      this.getApi();
    },
    async deleteApi(id){
      await axios.delete(apiUrl+id).then((resp) => {console.log(resp)});
      this.getApi();
    },
    async putApi(id){
      await axios.put(apiUrl+id,{"id":id,"firstName":this.firstName,"lastName":this.lastName}).then((resp) => {console.log(resp)});
      this.getApi();
    }
  },
  mounted(){
    this.getApi();
  }
}
</script>

<style>
html
{
  height: 100%;
}
body {
background: linear-gradient( #ededf0fa, #ec0808 );
padding: 0;
margin: 0;

}

h1{
  color: white;
}

.Contenedor {
  margin: 50px auto;
  padding: 30px;
  width: 400px;
  border-radius: 15px;
  background: rgba(0, 0, 0, 0.4);
}
</style>
