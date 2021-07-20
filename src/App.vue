<template>
  <v-app class="main-view">
    <v-app-bar app dense absolute color="deep-purple accent-4" dark shrink-on-scroll >
      <v-toolbar-title>Dalasito Wiki 📖</v-toolbar-title>

      <template v-slot:extension>
        <v-tabs align-with-title>
          <v-tab @click="getData('persona')">Personas 👨‍💼</v-tab>
          <v-tab @click="getData('animal')">Animales 🐕</v-tab>
          <v-tab @click="getData('objeto')">Objetos 🪑</v-tab>
        </v-tabs>
      </template>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row justify="center">
          <template v-for="(item, i) in actualItems">
            <v-col :key="i" cols="12" md="2" align="center">
              <v-hover v-slot="{ hover }">
                <v-card
                  height="200px"
                  width="200px"
                  :elevation="hover ? 12 : 2"
                  :class="{ 'on-hover': hover }"
                >
                  <v-img :src="item.img" height="200px" width="200px" @click="loadCharacterInfo(item.name)">
                    <v-card-title class="text-h6 white--text">
                      <v-row
                        class="fill-height flex-column"
                        justify="space-between"
                      >
                        <p class="mt-4 text-center text-border">
                          {{ item.name }}
                        </p>
                      </v-row>
                    </v-card-title>
                  </v-img>
                </v-card>
              </v-hover>
            </v-col>
          </template>
        </v-row>
      </v-container>
    </v-main>
    <p align="center" class="footer">2021 Raúl Moreno</p>

     <v-row justify="center" v-if="selectedCharacter != null" >
      <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition" >
        <v-card class="detail-view" >
          <v-toolbar dark color="deep-purple accent-4">
            <v-btn icon dark @click="dialog = false">
              <v-icon>mdi-close</v-icon>
            </v-btn>
            <v-toolbar-title>Detalles</v-toolbar-title>
          </v-toolbar>

          <v-list three-line subheader class="detail-view " align="center" >
         
          <v-list-item >
            <v-list-item-content >
              <v-list-item-title  class="white--text">Nombre</v-list-item-title>
              <v-list-item-subtitle  class="white--text">{{selectedCharacter.name}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="white--text">Genero</v-list-item-title>
              <v-list-item-subtitle class="white--text">{{selectedCharacter.gender}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="white--text">Fecha de nacimiento</v-list-item-title>
              <v-list-item-subtitle class="white--text">{{selectedCharacter.born}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="white--text">Raza</v-list-item-title>
              <v-list-item-subtitle class="white--text">{{selectedCharacter.race}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

           <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="white--text">Descripcion</v-list-item-title>
              <p class="ps-12 pt-4 white--text">{{selectedCharacter.description}}</p>
            </v-list-item-content>
          </v-list-item>

         

        </v-list>
        
          
        </v-card>
      </v-dialog>
    </v-row>
  </v-app>
</template>

<script>

import {items} from './dataSource'
export default {
  name: "App",
  data() {
    return {
      actualItems : [],
      selectedTab : "persona",
      dialog: false,
      selectedCharacter: null 
    };
  },
  mounted(){
    this.getData("persona")
  },
  methods:{
    getData(selectedTab){
      this.actualItems = items
      const filteredItems = []
      this.actualItems.forEach(element => {
        if(element.type == selectedTab){
          filteredItems.push(element)
        }
      });
      this.actualItems = filteredItems
      
    },
    loadCharacterInfo(name){
      this.dialog = true
      items.forEach(element => {
        if (element.name == name){
         var selectedCharacter = element
         this.selectedCharacter = selectedCharacter
        }
        
      });
      
    }
  }
};
</script>

<style>
.v-card {
  transition: opacity 0.3s ease-in-out;
}

.main-view{
  background-color: rgb(61, 61, 61) !important; 
}

.detail-view{
   background-color: rgb(61, 61, 61) !important; 
}

.text-border {
  -webkit-text-stroke: 0.5px black !important;
}

.footer {
  padding: 20px;
  color: white;
}


</style>
