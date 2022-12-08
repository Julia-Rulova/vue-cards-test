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

    <ul class="cards">
      <div class="card" v-for="card in cards" :key="card.id">
        <img class="card__img" :src="card.imageUrl" alt="card.name" />
        <h3 class="card__name">{{card.name}}</h3>
        <p class="card__description">{{card.description}}</p>
        <p class="card__price">{{card.price.toLocaleString()}} руб.</p>
        <button class="card__delete-btn" type="button" />
      </div>
    </ul>
  </section>
</template>

<script>
  import cardsList from "../static/cards.json";

  export default {
    data() {
      return {
        cards: cardsList
      }
    },
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

  .card {
    width: 100%;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    text-align: left;
    padding-bottom: 24px;
    position: relative;
  }

  .card__img {
    width: 100%;
    max-height: 200px;
    object-fit: cover;
  }

  .card__name {
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    color: #3F3F3F;
    margin: 16px;
    padding: 0;
    overflow-wrap: anywhere;
  }

  .card__description {
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    color: #3F3F3F;
    margin: 0 16px 62px;
    overflow-wrap: anywhere;
    display: -webkit-box;
    -webkit-line-clamp: 6;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .card__price {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: #3F3F3F;
    position: absolute;
    left: 16px;
    bottom: 24px;
  }

  .card__delete-btn {
    width: 32px;
    height: 32px;
    background-color: #FF8484;
    padding: 9px;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    transition: all 0.5s ease-in-out;
    position: absolute;
    top: -8px;
    right: -8px;
    background-image: url("../static/images/delete.svg");
    background-repeat: no-repeat;
    background-position: center;
    background-size: 16px;
    border: none;
  }

  .card__delete-btn:hover {
    cursor: pointer;
    opacity: 0.7;
    transition: all 0.5s ease-in-out;
  }

  .card__delete-btn:focus-visible {
    outline: none;
  }
</style>
