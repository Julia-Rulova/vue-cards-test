<template>
  <section class="app">
    <button class="app__open-popup" v-if="width < 1095" @click="openPopup">Добавить котика</button>
    <form-component v-else @create="createCard" />
    <cards-component :cards="cards" @remove="removeCard" />

    <popup-component :show="isPopupOpen" @hide="hidePopup">
      <form-component @create="createCard" />
    </popup-component>
  </section>
</template>

<script>
  import FormComponent from './FormComponent.vue';
  import CardsComponent from './CardsComponent.vue';
  import PopupComponent from './PopupComponent.vue';
  import cardsList from "../assets/cards.json";

  export default {
    components: { FormComponent, CardsComponent, PopupComponent },
    data() {
      return {
        cards: cardsList,
        width: innerWidth,
        isPopupOpen: false
      }
    },
    methods: {
      createCard(card) {
        card.id = this.cards.length;
        this.cards.unshift(card);
        localStorage.setItem("cards", JSON.stringify(this.cards));
        this.isPopupOpen = false;
      },
      removeCard(card) {
        this.cards = this.cards.filter(c => c.id !== card.id);
        localStorage.setItem("cards", JSON.stringify(this.cards));
      },
      updateWidth() {
        this.width = window.innerWidth;
      },
      openPopup() {
        this.isPopupOpen = true;
      },
      hidePopup() {
        this.isPopupOpen = false;
      }
    },
    beforeMount() {
      const cardsArr = localStorage.getItem("cards")
      if (cardsArr) {
        this.cards = JSON.parse(cardsArr)
      }
    },
    created() {
      window.addEventListener('resize', this.updateWidth);
    },
  }
</script>

<style>
  @font-face {
    font-family: 'Source Sans Pro';
    src: url("../assets/fonts/SourceSansPro-Regular.woff") format("woff"),
      url("../assets/fonts/SourceSansPro-Regular.woff2") format("woff2");
  }

  * {
    font-family: 'Source Sans Pro';
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    width: 100%;
    max-width: 1440px;
    height: 100%;
    margin: 32px auto;
    padding: 0 32px;
    background-color: rgba(255, 254, 251, 0.8);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    position: relative;
  }

  .app__open-popup {
    background: #FFFEFB;
    color: #B4B4B4;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    width: 150px;
    height: 36px;
    margin: 0;
    padding: 10px 16px;
    position: fixed;
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
    top: 32px;
    z-index: 2;
    transition: all 0.5s ease-in-out;
  }

  .app__open-popup:focus-visible {
    outline: none;
  }

  @media screen and (max-width: 1410px) {
    .app {
      max-width: 1095px;
    }
  }

  @media screen and (max-width: 1095px) {
    .app {
      flex-direction: column;
      justify-content: center;
      max-width: 920px;
    }
  }

  @media screen and (max-width: 750px) {
    .app {
      max-width: 720px;
    }
  }

  @media screen and (max-width: 550px) {
    .app {
      max-width: 320px;
      padding: 0;
    }

    .app__open-popup {
      bottom: 32px;
      top: auto;
      right: 32px;
    }

    .app__open-popup:hover {
      box-shadow: 0px 5px 20px 10px rgba(34, 60, 80, 0.2);
      cursor: pointer;
      transition: all 0.5s ease-in-out;
    }
  }
</style>