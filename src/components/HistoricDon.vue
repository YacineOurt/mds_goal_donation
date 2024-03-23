<template>
  <div class="historique-don">
    <div ref="historique" class="historique">
      <div v-for="don in historique" :key="don.id" class="don">{{ don.montant }}€</div>
    </div>
    <div class="nouveau-don">
      <input type="number" v-model="nouveauMontant" placeholder="" @keyup.enter="ajouterDon">
      <button @click="ajouterDon">Ajouter</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HistoriqueDon',
  data() {
    return {
      historique: [],
      nouveauMontant: ''
    };
  },
  methods: {
    ajouterDon() {
      const montant = parseInt(this.nouveauMontant);
      if (!isNaN(montant) && montant > 0) {
        this.historique.push({ id: Date.now(), montant });
        this.nouveauMontant = '';
        this.$emit('don-ajoute', montant); // Émettre l'événement 
        this.$nextTick(() => {
          this.$refs.historique.scrollTop = this.$refs.historique.scrollHeight;
        });
      } else {
        alert("Veuillez entrer un montant de don valide.");
      }
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

.historique-don {
  display: flex;
  flex-direction: column;
  height: 300px;
  width: 400px;
}
  .historique {
    flex: 1;
    overflow-y: scroll;
    border-radius: 3px;
    padding: 10px;
    overflow: hidden;
    background-color: #f3e3dc;
  }
  
  .don {
    margin-bottom: 5px;
    display: flex;
    flex-direction: row;
    color:#6F5B3E;
    font-family: "Poppins", sans-serif;
    font-style: normal;
    font-weight: 800;
  }
  
  .nouveau-don {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #f3e3dc;
    border-radius: 5px;
    height: 20%;
    widows: 100%;
    border-top: 3px solid  #37d540;
  }
  
  .nouveau-don input[type="number"] {
    width: 80%;
    height: 90%;
    outline: none;
    border: none;
    border-radius: 5px;
    -webkit-appearance: none;
    margin: 0;
    -moz-appearance: textfield;
    font-size: 20px;
    text-align: center;
    background-color: #f3e3dc;
  }
  
  .nouveau-don button {
    height: 100%;
    width: 40%;
    background-color: #37d540;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 20px;
    border-top: 3px solid  rgba(130, 242, 105, 0.504);

  }
  custom {
    font-size: 20px;
  }
  </style>
  