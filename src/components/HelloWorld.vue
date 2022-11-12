<template>
  <v-container>
    <v-app>
      <template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            Surname
          </th>
          <th>
            Age
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in daniels"
          :key="item.Id"
        >
          <td>{{ item.Name }}</td>
          <td>{{ item.Surname }}</td>
          <td>{{item.Age}}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  <br>
  <hr>
  <h2>INSERT NEW DANIEL</h2>
  <input type="text" v-model="name" placeholder="insert name">
  <input  type="text" v-model="surname" placeholder="insert surname">
  <input type="number" v-model="age" placeholder="insert age">
  <br>
  <v-btn @click="postDaniel">INSERT DANIEL</v-btn>
</template>

    </v-app>
  </v-container>
</template>

<script>
  import {getAXS,postDanielsAXS} from '@/services.js'
  
  export default {
    name: 'HelloWorld',

    data: () => ({
      daniels : [],
      name : '',
      surname : '',
      age : '',
      daniel : '',
    }),
    mounted(){
      this.getDaniels();
    },
    methods:{
      getDaniels(){
        getAXS("daniel").then(response=>{
          this.daniels = response.data;
        });
      },
      postDaniel(){
        postDanielsAXS(this.name,this.surname,this.age).then(response=>{
          this.daniel = response.data;
          alert("Daniel inserted");
        }).catch(error=>{
          alert("Daniel non inserted. ERROR: " + error.message)
        });
      }
    }
  }
</script>
