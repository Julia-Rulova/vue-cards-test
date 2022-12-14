<template>
    <div class="popup" v-if="show" @click.stop="$emit('hide')">
        <div @click.stop class="popup__container">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            show: Boolean
        }
    }
</script>

<style scoped>
    .popup {
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background: rgba(0, 0, 0, 0.5);
        position: fixed;
        display: flex;
        z-index: 3;
    }

    .popup__container {
        max-width: 80%;
        background: #fff;
        border-radius: 4px;
        margin: auto;
        z-index: 4;
    }

    @media screen and (max-width: 550px) {
        .popup__container {
            width: 80%;
            background: #fff;
            border-radius: 4px;
            margin: auto;
            z-index: 4;
        }
    }

    @media screen and (max-width: 355px) {
        .popup__container {
            width: 100%;
            background: #fff;
            border-radius: 4px;
            margin: auto;
            z-index: 4;
        }
    }
</style>