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
          class="mt-6"
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
<v-btn class="ma-0" tile color="pink" dark @click="deleteAll">Eliminar todo</v-btn>
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
      <v-tabs
        v-for="(item, index) in productsDetails" :key="index"
        dark
        color="pink"
        grow
      >
        <v-tab style="min-width: 0;">
          <v-badge
            color="deep-purple accent-4"
            :content="item.boxPrice"
            offset-x="40"
            offset-y="1"
          >
            <span style="background:red; color:white; border-radius: 50%;" class="mr-1 pa-1">{{ index +1 }}</span>{{ item.name }}
          </v-badge>
        </v-tab>

        <v-tab style="min-width: 0;">
          <v-badge
            color="pink"
            :content="item.qtyItems"
            overlap
            offset-x="20"
          >
            <v-icon size="24" dark>mdi-cart</v-icon>
          </v-badge>
        </v-tab>

        <v-tab style="min-width: 0;">
            <v-icon size="24" dark>mdi-close-outline</v-icon>
        </v-tab>

        <v-tab style="min-width: 0;">
          <v-badge
            color="pink"
            :content="item.priceByItems"
            overlap
            offset-x="20"
          >
            <v-icon size="24" dark>mdi-currency-usd-circle-outline</v-icon>
          </v-badge>
        </v-tab>

        <v-tab style="min-width: 0;">
            <v-icon size="24" dark>mdi-equal</v-icon>
        </v-tab>

        <v-tab style="min-width: 0;">
          <v-badge
            color="blue-grey"
            :content="item.total"
            overlap
            offset-x="20"
          >
            <v-icon size="24" dark>mdi-cash-remove</v-icon>
          </v-badge>
        </v-tab>

        <v-tab style="min-width: 0;">
          <v-badge
            color="red"
            :content="item.entryForItem"
            overlap
            offset-x="20"
          >
            <v-icon size="24" dark>mdi-cash-refund</v-icon>
          </v-badge>
        </v-tab>

        <v-tab @click="removeItemOfProductsDetails(item)" style="min-width: 0;">
          <v-icon color="red" size="24" dark>mdi-delete</v-icon>
        </v-tab>
      </v-tabs>
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
      entryForItem: '',
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
    created() {
      let arr = localStorage.getItem('itemArr');
      if (arr === null){
        this.productsDetails = [];
      } else {
        this.productsDetails = JSON.parse(arr);
      }
    },
    methods: {
      deleteAll() {
        this.productsDetails = [];
        localStorage.removeItem('itemArr');
      },
      removeItemOfProductsDetails(item) {
        this.productsDetails = this.productsDetails.filter(x => {
          return x !== item
        })
        localStorage.setItem('itemArr', JSON.stringify(this.productsDetails));
      },

      entryForItemM() {
        let entryForItem = Number(this.addedOperation) - Number(this.boxPrice);
        this.entryForItem = entryForItem.toFixed(2);
      },

      passiveM() {
        let passive = '';
        for(const index in this.productsDetails){
          passive = Number(passive) + Number(this.productsDetails[index].boxPrice);
        }
        this.passive = passive;
        this.passive ? passive.toFixed(2) : '';
      },

      addedOperationM() {
        let addedOperation = this.qtyItems * this.priceByItems;
        this.addedOperation = addedOperation.toFixed(2);
      },

      heritageM() {
        let heritage = '';
        for(const index in this.productsDetails){
          heritage = Number(heritage) + Number(this.productsDetails[index].total)
        }
        this.heritage = heritage;
        this.heritage ? this.heritage.toFixed(2) : '';
      },

      totalEarningsM(){
        let totalEarnings = this.heritage - this.passive;
        this.totalEarnings = totalEarnings.toFixed(2);
      },

      entryM() {
        let entry = (this.totalEarnings / 100) * 90;
        this.entry = entry.toFixed(2);
      },

      titheM() {
        let tithe = (this.totalEarnings / 100) * 10;
        this.tithe = tithe.toFixed(2);
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
          this.entryForItemM();
          resource.entryForItem = this.entryForItem;

          this.productsDetails.push(resource);
          localStorage.setItem('itemArr', JSON.stringify(this.productsDetails));

          this.nameItem = '';
          this.boxPrice = '';
          this.qtyItems = '';
          this.priceByItems = '';
        } else {
          let alertError = {
            dialog: true,
            buttonClose: 'Cerrar',
            title: 'Atención',
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


 .v-slide-group__prev--disabled{
   /* display: none!important; */
 }
</style>