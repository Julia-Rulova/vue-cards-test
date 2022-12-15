<template>
  <section class="cards__section">
    <div class="cards__select-right">
      <div class="cards__custom-select">
        <div class="cards__select-arrow" />
        <select class="cards__select" v-model="selectValue" @input="changeSelectValue">
          <option>По умолчанию</option>
          <option>Сначала недорогие</option>
          <option>Сначала дорогие</option>
          <option>По алфавиту</option>
        </select>
      </div>
    </div>

    <preloader-component v-if="loading" />

    <TransitionGroup name="cards-list" tag="ul" class="cards" v-else>
      <card-component v-for="card in cards" :card="card" :key="card.id" @remove="$emit('remove', card)" />
    </TransitionGroup>

  </section>
</template>

<script>
  import CardComponent from "./CardComponent.vue";
  import PreloaderComponent from './PreloaderComponent.vue';

  export default {
    props: {
      cards: Array,
      loading: Boolean
    },
    data() {
      return {
        selectValue: 'По умолчанию'
      }
    },
    components: { CardComponent, PreloaderComponent },
    methods: {
      changeSelectValue(evt) {
        if (evt.target.value === 'Сначала дорогие') {
          const sorted = this.cards.sort((c1, c2) => c1.price < c2.price ? 1 : -1);
        } else if (evt.target.value === 'Сначала недорогие') {
          const sorted = this.cards.sort((c1, c2) => c1.price > c2.price ? 1 : -1);
        } else if (evt.target.value === 'По алфавиту') {
          const sorted = this.cards.sort((c1, c2) => c1.name > c2.name ? 1 : -1);
        } else {
          const sorted = this.cards.sort((c1, c2) => c1.id < c2.id ? 1 : -1);
        }
      }
    }
  }
</script>

<style scoped>
  .cards__section {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 55px;
    width: 100%;
  }

  .cards__select-right {
    position: absolute;
    top: 0;
    right: 32px;
    height: 36px;
  }

  .cards__custom-select {
    background: #FFFEFB;
    color: #B4B4B4;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    width: 150px;
    height: 36px;
    padding: 10px 10px 10px 16px;
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    transition: all 0.5s ease-in-out;
  }

  .cards__custom-select:hover {
    box-shadow: 0px 5px 39px 2px rgba(34, 60, 80, 0.2);
    transition: all 0.5s ease-in-out;
  }

  .cards__select-arrow {
    background-image: url("../assets/images/arrow.svg");
    background-size: cover;
    background-repeat: no-repeat;
    width: 15px;
    height: 12px;
    opacity: 0.5;
  }

  .cards__select {
    outline: none;
    appearance: none;
    border: none;
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #B4B4B4;
    width: 100%;
    height: 100%;
    padding: 0 10px 0 16px;
    background-color: transparent;
    position: absolute;
    top: 0;
    right: 0;
    cursor: pointer;
  }

  .cards__select:focus-visible {
    outline: none;
  }

  .cards {
    display: grid;
    grid-template-columns: repeat(3, 332px);
    grid-gap: 16px;
  }

  .cards-list-move,
  .cards-list-enter-active,
  .cards-list-leave-active {
    transition: all 0.5s ease;
  }

  .cards-list-enter-from,
  .cards-list-leave-to {
    opacity: 0;
    transform: scale(0.6);
  }

  .cards-list-leave-active {
    position: absolute;
  }

  @media screen and (max-width: 1410px) {
    .cards {
      grid-template-columns: repeat(2, 332px);
    }
  }

  @media screen and (max-width: 1095px) {
    .cards {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media screen and (max-width: 750px) {
    .cards {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media screen and (max-width: 550px) {
    .cards {
      grid-template-columns: repeat(1, 1fr);
    }

    .cards__section {
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
      padding-top: 50px;
    }

    .cards__custom-select {
      width: 140px;
      padding: 7px 7px 7px 10px;
    }

    .cards__select {
      padding: 0 7px 0 10px;
    }

    .cards__select-right {
      right: 0;
    }
  }

  @media screen and (max-width: 355px) {
    .cards__section {
      padding: 48px 10px 0;
    }

    .cards__select-right {
      right: 10px;
      height: 32px;
    }

    .cards__custom-select {
      height: 32px;
    }
  }
</style>