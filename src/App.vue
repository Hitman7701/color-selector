<script setup>
// Import du fichier JSON
import colorsList from './assets/data/colorsList'

import { ref } from 'vue'

// Création de la valeur réactive qui stocke la couleur sélectionnée
const selectedColor = ref('rgb(245, 245, 245)')

const selectColor = (color) => {
  selectedColor.value = color
}

// Fonction qui copie dans le presse-papier
const copyToClipboard = async () => {
  try {
    // Copier dans le presse-papiers est une action asynchrone, donc on utilise le async/await pour déclencher l'alerte seulement une fois l'action réalisée
    await navigator.clipboard.writeText(selectedColor.value)
    alert(`'${selectedColor.value}' has been copied'`)
  } catch (error) {
    // On utilise également un try/catch pour afficher l'erreur en cas de problème avec l'action asynchrone
    alert('Cannot copy', error)
  }
}
</script>

<template>
  <main>
    <h1>Sélectionnez une couleur</h1>

    <div>
      <section class="leftCol">
        <!-- Boucle sur le tableau pour accéder à chaque sous-tableau -->
        <div v-for="subColorsList in colorsList" :key="subColorsList[0]">
          <!-- Boucle sur le sous-tableau pour accéder à chaque couleur -->
          <div
            v-for="color in subColorsList"
            :key="color"
            :style="{ backgroundColor: color }"
            @click="selectColor(color)"
            :class="{
              selected: color === selectedColor,
            }"
          ></div>
          <!-- Cette 'div' a du style dynamique qui affiche en arrière plan la couleur et une classe CSS dynamique qui s'affiche seulement s'il s'agit de la couleur sélectionnée -->
        </div>
      </section>

      <section class="rightCol">
        <!-- Affichage de la valeur de la couleur sélectionnée -->
        <p @click="copyToClipboard">{{ selectedColor }}</p>

        <!-- Bloc dans lequel est affiché la couleur sélectionnée -->
        <div @click="copyToClipboard"></div>
      </section>
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  padding: 50px;
}
main > div {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 150px;
  flex: 1;
}
/* -- Colonne de gauche -------- */
.leftCol {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.leftCol > div {
  display: flex;
  gap: 10px;
}
.leftCol > div > div {
  height: 50px;
  width: 50px;
  border-radius: 3px;
  cursor: pointer;
}
/* -- Colonne de droite --------- */
.rightCol > div {
  background-color: v-bind(selectedColor);
  width: 300px;
  height: 300px;
  border-radius: 5px;
  cursor: pointer;
}
p {
  text-align: center;
  margin-bottom: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  cursor: pointer;
}
/* -- Autre --------- */
.selected {
  box-shadow: 0px 0px 10px black;
}
</style>
