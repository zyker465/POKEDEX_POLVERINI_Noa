<template>
  <!-- div contenant toutes les détails du pokemon -->
  <div  class="detail">
    <div class="detail-view card">
      <div class="data card-body">
        <!-- image du pokemon -->
        <img class="image" v-bind:src="donnees.sprites.front_default" />

        <!-- Nom du pokemon -->
        <h2 class="card-title">{{name}}</h2>

        <!-- types du pokemon -->
        <div class="types" v-for="item in donnees.types" :key="item.slot">
          <div class="type">
            <span :class="item.type.name">{{item.type.name}}</span>
          </div>
        </div>

        <!-- abilité du pokemon -->
        <div class="abilities" v-for="item in donnees.abilities" :key="item.ability.name">
          <div class="ability">{{item.ability.name}}</div>
        </div>

        <!-- propriétés du pokemon -->
        <div class="property">
          <div class="left bold">Taille et Poids</div>
          <div class="right">{{donnees.height}}cm {{donnees.weight}}kg</div>
        </div>

      </div>

      <!-- bouton fermer pour fermer les détails -->
      <button class="close" v-on:click="fermerDetails">Fermer</button>
    </div>
  </div>
</template>

<script>

// import 
import axios from 'axios';
export default {
  // déclaration des props
  props: ["name","url"],

  // création d'un beforeMount 
  beforeMount() {    
    axios
      .get(this.url)
      .then((response)=>{
        this.donnees = response.data
      })
  },

  // déclaration du data
  data: function(){
      return {
        donnees : [],
      }
  },

  // déclaration des méthodes
  methods: {
    // méthodes pour fermer détails
    fermerDetails () { 
      this.$emit("close")
    },
  },
};
</script>

<!-- style de la page -->
<style lang="scss" scoped>
.type {
  .grass {
    background: rgb(3, 139, 44) !important;
  }
  .poison {
    background: rgb(74, 7, 105) !important;
  }
  .water {
    background: rgb(8, 135, 219) !important;
  }
  .dragon {
    background: rgb(27, 2, 68) !important;
  }
  .ice {
    background: rgb(78, 199, 255) !important;
  }
  .flying {
    background: rgb(145, 215, 255) !important;
  }
  .fire {
    background: rgb(238, 135, 17) !important;
  }
  .ghost {
    background: rgb(74, 52, 87) !important;
  }
  .fighting {
    background: rgb(122, 0, 0) !important;
  }
  .normal {
    background: rgb(104, 104, 104) !important;
  }
  .psychic {
    background: rgb(195, 0, 255) !important;
  }
  .bug {
    background: rgb(52, 87, 6) !important;
  }
  .dark {
    background: rgb(43, 43, 43) !important;
  }
  .steel {
    background: rgb(116, 116, 116) !important;
  }
  .fairy {
    background: rgb(248, 165, 237) !important;
  }
  .eletric {
    background: rgb(255, 217, 1) !important;
  }
  .rock {
    background: rgb(88, 95, 100) !important;
  }
  .ground {
    background: rgb(92, 70, 70) !important;
  }
}

.detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  //width: calc(100% - 20px);
  // height: calc(100vh - 20px);
  width: 100%;
  height: 100vh;
  background: rgba(10, 7, 0, 0.562);
}
.detail-view {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 90%;
  padding: 50px 0 0;
  position: relative;

  max-width: 510px;

  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
.image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 120px;
  height: 120px;
  background-color: #ffcb04;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

h2 {
  text-transform: capitalize;
}

.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 40px;
}
.property {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  margin-bottom: 10px;
}
.left {
  float: left;
}
.right {
  float: right;
}
h3 {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
}

.types,
.abilities {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 90%;
  max-width: 400px;
}
.type {
  // color: rgb(17, 67, 182);
  margin: 0 0 10px 0;
  padding: 5px 10px;
  margin-left: -10px;
  font-weight: bold;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  span {
    color: #ffffff !important;
    padding: 10px 14px;
    border-radius: 29px;
  }
}
.ability {
  color: rgb(10, 119, 10);
  margin: 0 10px 10px 0;
  border-radius: 20px;
  padding: 5px 10px;
  font-weight: bold;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  word-wrap: none;
  word-break: keep-all;
  background-color: #ffffff;
  border: 3px solid;
}

.close {
  outline: none;
  border: none;
  border-radius: 5px;
  background-color: #c73015;
  color: #efefef;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 1.2rem;
  cursor: pointer;
}
i {
  font-size: 2rem;
  color: #efefef;
}
.bold {
  font-weight: bold;
}
</style>
