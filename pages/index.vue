<template>
  <v-app id="sandbox">
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      temporary
      app
      overflow
    ></v-navigation-drawer>

    <v-app-bar
      app
    >
      <v-app-bar-nav-icon
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
      ></v-app-bar-nav-icon>
      <v-toolbar-title>Tienda doña florencia</v-toolbar-title>
      <v-spacer></v-spacer>
        <v-switch
          v-model="$vuetify.theme.dark"
          color="pink"
          class="mt-4"
        ></v-switch>


        <template v-slot:extension>
            <v-btn
              @click="calculateOperation"
              fab
              color="pink"
              dark
              small
              bottom
              left
              absolute

            >
              <v-icon>mdi-plus</v-icon>
            </v-btn>



            <v-toolbar
              height="48"
            >
              <v-tabs
                grow
                color="pink"
              >

                <v-tab>
                  <v-badge
                    color="brown"
                    :content="tithe"
                    class="mr-4"
                  >
                    Diesmo
                  </v-badge>
                </v-tab>

                <v-tab>
                  <v-badge
                    color="purple"
                    :content="entry"
                  >
                    Activo
                  </v-badge>
                </v-tab>

                <v-tab>
                  <v-badge
                    color="red"
                    :content="totalEarnings"
                  >
                    neto
                  </v-badge>
                </v-tab>
              
                <v-tab>
                  <v-badge
                    color="blue-grey"
                    :content="heritage"
                  >
                    Patrimonio
                  </v-badge>
                </v-tab>

                <v-tab>
                  <v-badge
                    color="brown"
                    :content="passive"
                    class="mr-4"
                  >
                    Gastos
                  </v-badge>
                </v-tab>

              </v-tabs>
            </v-toolbar>




          </template>
    </v-app-bar>

    <v-form>
      <v-container>
        <v-row>
          <v-col
            cols="4"
          >
            <v-text-field
              v-model="nameItem"
              color="pink"
              label="Nombre"
              type="text"
              required
            ></v-text-field>
          </v-col>

          <v-col
            cols="3"
          >
            <v-text-field
              v-model="boxPrice"
              type="number"
              color="pink"
              label="caja"
              required
            ></v-text-field>
          </v-col>

          <v-col
            cols="2"
          >
            <v-text-field
              v-model="qtyItems"
              color="pink"
              type="number"
              label="unidades"
              required
            ></v-text-field>
          </v-col>

          <v-col
            cols="3"
          >
            <v-text-field
              v-model="priceByItems"
              type="number"
              label="precio por unidad"
              color="pink"
              required
            ></v-text-field>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
    
<Modal :alertError="alertError"/>

    <v-container class="pa-0">
      <div class="text-center" v-for="(item, index) in productsDetails" :key="index">
          <v-chip
            class="px-2 mr-0"
            color="pink"
            label
            text-color="white"
          >
            <v-avatar
              left
              class="green darken-4 mr-0"
            >
              <span class="white--text font-weight-black text-caption">{{ index + 1 }}</span>
            </v-avatar>
            {{ item.name }}
            <v-avatar right color="teal darken-4 ml-0">
              <span class="white--text font-weight-black text-caption">{{ item.boxPrice }}</span>
            </v-avatar>
          </v-chip>

          <v-avatar color="teal" size="36">
            <span class="white--text font-weight-black text-caption">{{ item.qtyItems }}</span>
          </v-avatar>

          <v-btn  fab dark x-small color="brown">
            <v-icon size="26">mdi-close-thick</v-icon>
          </v-btn>

          <v-avatar color="teal" size="36">
            <span class="white--text font-weight-black text-caption">{{ item.priceByItems }}</span>
          </v-avatar>

          <v-btn dark x-small fab color="red">
            <v-icon size="26" dark>mdi-equal</v-icon>
          </v-btn>

          <v-avatar color="secondary">
            <span class="white--text font-weight-black text-caption">{{ item.total }}</span>
          </v-avatar>

        </div>
    </v-container>

    <!-- <v-footer app :padless="true">
      <v-container class="pa-0">
        <div class="text-center">
          <v-chip
            class="px-2 mr-0"
            color="pink"
            label
            text-color="white"
          >
            <v-avatar
              left
              class="green darken-4 mr-0"
            >
              <span class="white--text font-weight-black text-caption">224</span>
            </v-avatar>
            mermelada
            <v-avatar right color="teal darken-4 ml-0">
              <span class="white--text font-weight-black text-caption">6423</span>
            </v-avatar>
          </v-chip>

          <v-avatar color="teal" size="36">
            <span class="white--text font-weight-black">224</span>
          </v-avatar>

          <v-btn  fab dark x-small color="brown">
            <v-icon size="26">mdi-close-thick</v-icon>
          </v-btn>

          <v-avatar color="teal" size="36">
            <span class="white--text font-weight-black">224</span>
          </v-avatar>

          <v-btn dark x-small fab color="red">
            <v-icon size="26" dark>mdi-equal</v-icon>
          </v-btn>

          <v-avatar color="secondary" size="36">
            <span class="white--text font-weight-black">2243</span>
          </v-avatar>
        </div>
      </v-container>
    </v-footer> -->
  </v-app>
</template>

<script>

import Modal from '~/components/modal';

  export default {
    components: {
      Modal
    },
    data: () => ({
      primaryDrawer: {
        model: null,
        type: 'default (no property)'
      },
      nameItem: '',
      boxPrice: '',
      qtyItems: '',
      priceByItems: '',
      totalEarnings: '',
      productsDetails: [],

      addedOperation: '',
      heritage: '',
      entry: '',
      tithe: '',
      passive: '',

      alertError: {}
    }),
    watch: {
      productsDetails: function(val){
        this.passiveM();
        this.heritageM();
        this.totalEarningsM();
        this.entryM();
        this.titheM();
      }
    },
    methods: {
      passiveM() {
        let passive = '';
        for(const index in this.productsDetails){
          passive = Number(passive) + Number(this.productsDetails[index].boxPrice);
        }
        this.passive = passive;
      },

      addedOperationM() {
        this.addedOperation = this.qtyItems * this.priceByItems;
      },
      heritageM() {
        let heritage = '';
        for(const index in this.productsDetails){
          heritage = Number(heritage) + Number(this.productsDetails[index].total)
        }
        this.heritage = heritage;
      },

      totalEarningsM(){
        this.totalEarnings = this.heritage - this.passive;
      },
      entryM() {
        this.entry = (this.totalEarnings / 100) * 90;
      },
      titheM() {
        this.tithe = (this.totalEarnings / 100) * 10;
      },

      calculateOperation(){
        if (this.nameItem && this.boxPrice && this.qtyItems && this.priceByItems)
        {
          this.addedOperationM();
          let resource = {
            name: this.nameItem,
            boxPrice: this.boxPrice,
            qtyItems: this.qtyItems,
            priceByItems: this.priceByItems,
            total: this.addedOperation
          }
          this.productsDetails.push(resource);

          this.nameItem = '';
          this.boxPrice = '';
          this.qtyItems = '';
          this.priceByItems = '';
        } else {
          let alertError = {
            dialog: true,
            buttonClose: 'Cerrar',
            title: 'Campo vacio',
            description: ''
          }
          if(!this.nameItem){
            alertError.description = 'Asigne un nombre para el producto'
          } else if (!this.boxPrice){
            alertError.description = `Con cuanto compraste una caja de ${this.nameItem }`
          } else if(!this.qtyItems){
            alertError.description = `Cuantos unidades tiene una caja de ${this.nameItem }`
          } else if(!this.priceByItems){
            alertError.description = `Cuanto vale cada unidad de ${this.nameItem }`
          }
          this.alertError = alertError;
        }
      }
    }
  }
</script>

<style>
 .v-toolbar__extension{
   padding: 0;
 } 

  .v-chip__content{
    letter-spacing: -.5px;
    font-size: 14px;
  }
 .v-chip__content .v-avatar {
   width: 28px !important;
 }
</style>