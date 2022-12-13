<template>
  <section class="cards__section">
    <div class="cards__custom-select">
      <div class="cards__select-arrow">🢓</div>
      <select class="cards__select">
        <option>По умолчанию</option>
        <option>По цене min</option>
        <option>По цене max</option>
        <option>По наименованию</option>
      </select>
    </div>


    <TransitionGroup name="cards-list" tag="ul" class="cards">
      <card-component v-for="card in cards" :card="card" :key="card.id" @remove="$emit('remove', card)" />
    </TransitionGroup>

  </section>
</template>

<script>
  import CardComponent from "./CardComponent.vue";

  export default {
    props: {
      cards: Array
    },
    components: { CardComponent }
  }
</script>

<style scoped>
  .cards__section {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }

  .cards__custom-select {
    background: #FFFEFB;
    color: #B4B4B4;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    width: 140px;
    height: 36px;
    margin-bottom: 19px;
    padding: 10px 16px;
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  .cards__select-arrow {
    width: 8px;
    height: 9px;
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
    padding: 0 16px;
    background-color: transparent;
    position: absolute;
    top: 0;
    right: 0;
    cursor: pointer;
  }

  .cards__select:focus-visible {
    outline: none;
  }

  .cards__select::after {
    content: "🢓";
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
</style>