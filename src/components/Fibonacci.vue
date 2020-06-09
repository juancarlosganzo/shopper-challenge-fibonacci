<template>
  <div >
     <b-card title="Fibonacci Anterior" >
         <b-card-text>Ingresa un numero entero para realizar el calculo de su número fibonacci anterior inmediato.</b-card-text>
         <b-container>
             <b-row>
                 <b-col  cols="4">
                     <b-form @submit.prevent="submit">
                         <b-input-group  class="mt-3">
                            <b-form-input id="valor" v-model="form.valor"></b-form-input>
                            <b-button variant="outline-success" type="submit"  >Calcular</b-button>
                        </b-input-group>
                        <br />
                        <b-alert variant="danger" :show="!$v.form.valor.required && this.form_submit ">Ingrese un número entero</b-alert>
                        <b-alert variant="danger" :show="!$v.form.valor.integer && this.form_submit">Debes ingresar un número entero</b-alert>
                        <b-alert variant="danger" :show="!$v.form.valor.maxValue && this.form_submit">El valor maximo es de 9500</b-alert>
                        
                    </b-form>
                 </b-col>
                 <b-col cols="8">
                 </b-col>
            </b-row>
         </b-container>
     </b-card>
     <b-modal id="msg-modal" title="Fibonacci Anterior" hide-footer>         
            <div class="d-block text-center">
                <h3>El Resultado es {{ result }}</h3>
            </div>
            <b-button class="mt-3" block @click="$bvModal.hide('msg-modal')">Cerrar</b-button>
    </b-modal>
  </div>
    
</template>

<script>
import { required,integer  } from 'vuelidate/lib/validators'
export default {
  name: 'Fibonacci',
   data(){
    return {
        form:{ valor:"" },
        result:"",
        form_submit:false
    };
  },
  validations:{
      form:{
          valor:{
              required,
              integer,
              maxValue: 9500
          }
      }

  },
  methods:{
    submit(){
        this.$v.$touch();
        this.form_submit = true
            if(!this.$v.$invalid){                
                this.result = this.fibonancci(this.form.valor,null);
                this.$bvModal.show("msg-modal");
            }

        }
    ,
    fibonancci(limite,temp){
        
         temp = temp || {};

        if(temp[limite]) return temp[limite];

        if(limite <= 1){
                return 1;
        }
        
        temp[limite] = this.fibonancci(limite-1,temp) + this.fibonancci(limite -2, temp);
        
        if(this.form.valor < temp[limite] ){
               temp[limite] = temp[limite-1];
        } 
     return temp[limite]
    }
  }
}
</script>
