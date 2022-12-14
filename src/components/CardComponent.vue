<template>
    <div class="card">
        <img class="card__img" :src="card.imageUrl" :alt="card.name" />
        <h3 class="card__name">{{card.name}}</h3>
        <p class="card__description">{{card.description}}</p>
        <p class="card__price">{{card.price.toLocaleString()}} руб.</p>
        <button class="card__delete-btn" type="button" @click="$emit('remove', card)" />
    </div>
</template>

<script>
    export default {
        props: {
            card: Object
        }
    }
</script>

<style scoped>
    .card {
        width: 332px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        text-align: left;
        padding-bottom: 24px;
        position: relative;
        transition: all 0.5s ease-in-out;
    }

    .card:hover .card__delete-btn {
        opacity: 1;
    }

    .card__delete-btn {
        opacity: 0;
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
        background-image: url("../assets/images/delete.svg");
        background-repeat: no-repeat;
        background-position: center;
        background-size: 16px;
        border: none;
    }

    .card:hover .card__delete-btn:hover {
        cursor: pointer;
        background-color: #FF5555;
        transition: all 0.5s ease-in-out;
    }

    .card__delete-btn:focus-visible {
        outline: none;
    }

    .card__img {
        width: 100%;
        max-height: 200px;
        object-fit: cover;
        border-radius: 10px 10px 0 0;
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
</style>