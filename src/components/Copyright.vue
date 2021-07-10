<template>
   <div >
      <b-container>
         <b-row>
            <b-col md="6" class="float-right">
               <b-form-group label="Select Chanel">
                  <b-form-select v-model="selectedChanel" @change="changeChanel()" class="select-chanel">
                     <b-form-select-option v-for="item in salesChanels" :value="item">
                        {{item.name}}
                     </b-form-select-option>
                  </b-form-select>
               </b-form-group>
               <b-form-group>
                  <b-button @click="addNewSales()" variant="primary">Add New Sales Chanel</b-button>
               </b-form-group>
            </b-col>
            <b-col md="6" class="float-right">
               <b-form-group 
                  label="Select Language">
                  <b-form-select v-model="selectedLanguage" @change="changeLanguage()" class="select-language">
                     <b-form-select-option v-for="item in selectedChanel.languages" :value="item">
                        {{item.name}}
                     </b-form-select-option>
                  </b-form-select>
               </b-form-group>
               <b-form-group>
                  <b-button @click="addNewCopyRight()" variant="primary">Add New Copyright Text</b-button>
               </b-form-group>
            </b-col>
         </b-row>
         <b-row class="form-section-group">
            <b-col md="6" class="sales-chanel">
               <div v-if="addNewSalesChanel">
                  <b-form-group class="form-name"
                     label="Sales Chanel Name" 
                     label-cols-md="4"
                     label-align-md="right">
                     <b-form-input type="text" name="" v-model="name"></b-form-input>
                  </b-form-group>
                  <b-form-group 
                     label="Color" 
                     label-cols-md="1"
                     label-align-md="right">
                     <b-form-input type="color"  name="" v-model="chanelColor"></b-form-input>
                  </b-form-group>
                  <b-form-group>
                     <b-button @click="addSales()" variant="primary" class="sales-btn">Add Sales Chanel</b-button>
                  </b-form-group>
               </div>
            </b-col>
            <b-col md="6"  class="language-section">
               <div v-if="addNewCopyRightParagraph">
                  <b-form-group class="form-name"
                     label="Language Name" 
                     label-cols-md="3"
                     label-align-md="right">
                     <b-form-input type="text"  v-model="languageName"></b-form-input>
                  </b-form-group>
                  <b-form-group 
                     label="Copyright Text"
                     label-cols-md="3"
                     label-align-md="right">
                     <b-form-input type="text"  v-model="newCopyRight"></b-form-input>
                  </b-form-group>
                  <b-form-group>
                     <b-button @click="addCopyRight()" variant="primary" class="copyright-btn">Add CopyRight</b-button>
                  </b-form-group>
               </div>
            </b-col>
         </b-row>
      </b-container>
      <br>
      <page-footer 
         :text="text"
         :color="color">    
      </page-footer>
   </div>
</template>

<script>
  import PageFooter from "./PageFooter";

export default {
  name: 'Copyright',
  data () {
    return {
      addNewSalesChanel: false,
      addNewCopyRightParagraph: false,
      text:null,
      color:null,
      languageName: null,
      salesChanels: [{
            name: 'Default',
            languages: [{
              name: 'Default',
              copyRightText: 'Copyright © signundsinn GmbH'
            }],
            color: '#eb4034',
      }],
      sales: this.initialState(),
      copyRightText: null,
      selectedChanel: null,
      name: 'Default',
      chanelColor: '#eb4034',
      languageName: 'Default',
      newCopyRight: 'Copyright © signundsinn GmbH',
      selectedLanguage: [],
    }    
  },

  components: {
    PageFooter,
  },

  mounted() {
      this.selectedChanel = this.salesChanels[0];
      this.selectedLanguage = this.selectedChanel.languages[0];
      this.text = this.selectedLanguage.copyRightText;
      this.color = this.selectedChanel.color;
  },

  methods:{
      initialState (){
        return {
              name: 'Default',
              languages: [{
                name: 'Default',
                copyRightText: 'Copyright © signundsinn GmbH'
          }],
              color: '#eb4034',
        }
      },

      addSales(){
        this.sales.name = this.name;
        this.sales.color =this.chanelColor;
        this.name = 'Default',
        this.chanelColor = '#eb4034',  
        this.salesChanels.push(this.sales);
        this.sales = this.initialState();
      },


      changeChanel(){
        this.text = this.selectedChanel.languages[0].copyRightText;
        this.color = this.selectedChanel.color;
        this.selectedLanguage = this.selectedChanel.languages[0];
      },

      addNewSales(){
          this.addNewSalesChanel = true;
      },

      addNewCopyRight(){
        this.addNewCopyRightParagraph = true;
      }, 

      addCopyRight(){
          let i=0;
          let abc=0;
          var valObj = this.salesChanels.filter(obj => {
              if(obj.name == this.selectedChanel.name){
                  abc=i;
              }
              else{
                i=i+1;
              }  
              
          });

          let data = {
            'name' : this.languageName,
            'copyRightText' : this.newCopyRight
          }

          this.salesChanels[abc].languages.push(data);
          this.languageName = 'Default';
          this.newCopyRight = 'Copyright © signundsinn GmbH';
          
      },

      changeLanguage() {
        this.text = this.selectedLanguage.copyRightText;      
      }
  },
}
</script>

<style scoped>
  .sales-chanel{
    margin-top:  20px;
  }

  .language-section{
    margin-top: 20px;
  }

  .select-chanel{
    width: 150px;
    height: 30px;
    margin-bottom: 25px;
  }

  .select-language{
    width: 150px;
    height: 30px;
    margin-bottom: 25px;
  }

  .sales-btn{
    float: left;
    margin-top: 25px;
  }

  .copyright-btn{
    float:  left;
    margin-top: 25px;
  }

  .form-section-group{
    margin-top: 30px;
  }

  .form-name{
    margin-bottom: 15px;
  }
</style>
