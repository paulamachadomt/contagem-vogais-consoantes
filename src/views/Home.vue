<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title> Contador de vogais e consoantes </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <ion-grid class="ion-padding">
        <ion-row>
          <ion-col>
            <ion-label
              >Digite o que quiser e clique em <b>enviar:</b></ion-label
            >
            <ion-input
              id="input-usuario"
              placeholder="digite aqui..."
              clearInput value=""
            ></ion-input>
          </ion-col>
        </ion-row>

        <ion-row class="ion-justify-content-center">
          <ion-col>
            <ion-button @click="acionarBotao()" expand="block" class="ion-margin-bottom"
              >Enviar</ion-button
            >
          </ion-col>
        </ion-row>        

        <ion-row>
          <ion-col id="resultado" 
            >{{ vogais }} vogais <br>
            {{ consoantes }} consoantes</ion-col
          >
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonLabel, IonInput, IonGrid, IonButton, IonRow, IonCol } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonLabel, 
    IonInput,
    IonGrid, 
    IonRow, 
    IonCol,
    IonButton
  },
  data() {
    return {         
      vogais: 0,
      consoantes: 0
    }
  },
  methods: {
    acionarBotao: function() {      
      this.contarVogaisConsoantes("input-usuario");
    },

    contarVogaisConsoantes: function(input) {                
      const elementoInput = document.getElementById(input);
      const palavra = elementoInput.value;
      
      const palavraSemNumeros = palavra.replace(/[1234567890]/ig, ''); //remove números
      const palavraSemCaracteresEspeciais = palavraSemNumeros.replace(/[^a-zA-ZÁÀÂÃÉÈÊÍÏÓÔÕÖÚÇÑ ]/ig, ''); //remove caracteres especiais
      const palavraSemEspacos = palavraSemCaracteresEspeciais.replace(/\s/g, ''); //remove espaços
      
      const palavraSemVogais = palavraSemEspacos.replace(/[aeiouÁÀÂÃÉÈÊÍÏÓÔÕÖÚ]/ig, ''); //remove as vogais da palavra "limpa"

      if (palavraSemVogais.length != 0){
        this.consoantes = palavraSemVogais.length; //sem as vogais, o tamanho do que sobra é o n° de consoantes
      }  
    
      const palavraSemConsoantes = palavraSemEspacos.replace(/[BCDFGHJKLMNPQRSTVXWYZ]/ig, ''); //remove as consoantes da palavra "limpa"

      if(palavraSemConsoantes.length != 0) {
        this.vogais = palavraSemConsoantes.length; //sem as consoantes, o tamanho do que sobra é o n° de vogais
      }      

    },    
          
  }
});
</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}

#input-usuario {
  margin-top: 10px;
  border: 1px solid lightgray;
  border-radius: 5px;
}

</style>