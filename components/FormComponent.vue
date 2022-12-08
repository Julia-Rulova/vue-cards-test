<template>
  <section class="form__section">
    <h1 class="form__title">Добавление товара</h1>

    <form class="form" @submit.prevent>
      <div class="form__input-container">
        <div class="form__label-container">
          <label class="form__input-label" for="name">Наименование товара</label>
          <div class="form__input-required" />
        </div>
        <input class="form__input" :class="{'form__input_error': nameError}" v-model="name" id="name"
          placeholder="Введите наименование товара" @input="validateName" type="text" maxlength="40" />
        <span class="form__input-error">{{nameError}}</span>
      </div>

      <div class="form__input-container">
        <label class="form__input-label" for="description">Описание товара</label>
        <textarea class="form__input form__input_textarea" v-model="description" id="description"
          placeholder="Введите описание товара" maxlength="240" />
      </div>

      <div class="form__input-container">
        <div class="form__label-container">
          <label class="form__input-label" for="imageUrl">Ссылка на изображение товара</label>
          <div class="form__input-required" />
        </div>
        <input class="form__input" :class="{'form__input_error': imageUrlError}" v-model="imageUrl" id="imageUrl"
          placeholder="Введите ссылку" type="url" @input="validateUrl" />
        <span class="form__input-error">{{imageUrlError}}</span>
      </div>

      <div class="form__input-container">
        <div class="form__label-container">
          <label class="form__input-label" for="price">Цена товара</label>
          <div class="form__input-required" />
        </div>
        <input class="form__input" :class="{'form__input_error': priceError}" v-model="price" id="price"
          placeholder="Введите цену" type="number" min="1" @input="validatePrice" />
        <span class="form__input-error">{{priceError}}</span>
      </div>

      <button type="submit" class="form__submit-btn"
        :class="{'form__submit-btn_active':(name !== '') & (imageUrl !== '') & (imageUrlError === '') & (price > 0)}"
        @click="handleSubmit" disabled="true">Добавить
        товар</button>
    </form>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        name: "",
        nameError: "",
        description: "",
        imageUrl: "",
        imageUrlError: "",
        price: null,
        priceError: ""
      }
    },
    methods: {
      validateName(evt) {
        if (evt.target.value.length < 2 || evt.target.value.length > 40) {
          this.nameError = "Название должно содержать от 2 до 40 символов";
        } else {
          this.nameError = "";
        }
      },
      validateUrl(evt) {
        const reg = /[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)?/gi;
        if (!reg.test(evt.target.value) || !evt.target.value) {
          this.imageUrlError = "Некорректный формат ссылки";
        } else {
          this.imageUrlError = "";
        }
      },
      validatePrice(evt) {
        if (!evt.target.value || evt.target.value < 1) {
          this.priceError = "Введите цену товара";
        } else {
          this.priceError = "";
        }
      },
      handleSubmit(evt) {
        this.name = "";
        this.description = "";
        this.imageUrl = "";
        this.price = "";
      }
    }
  }
</script>

<style scoped>
  .form__section {
    display: flex;
    flex-direction: column;
    margin-right: 16px;
    width: 332px;
  }

  .form__title {
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
    color: #3F3F3F;
    text-align: left;
    margin: 0 0 16px;
    padding: 0;
  }

  .form {
    width: 100%;
    padding: 24px;
    background-color: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    position: sticky;
    top: 24px;
  }

  .form__input-container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    margin-bottom: 16px;
    position: relative;
  }

  .form__input-container:last-of-type {
    margin-bottom: 24px;
  }

  .form__label-container {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-start;
    margin-bottom: 4px;
  }

  .form__input-label {
    font-style: normal;
    font-weight: 400;
    font-size: 13px;
    line-height: 15px;
    letter-spacing: -0.02em;
    color: #49485E;
  }

  .form__input-required {
    width: 4px;
    height: 4px;
    background: #FF8484;
    border-radius: 4px;
  }

  .form__input {
    width: 100%;
    height: 36px;
    background-color: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border: none;
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #3F3F3F;
    padding: 10px 16px;
  }

  .form__input_error {
    border: 1px solid #FF8484;
    color: #FF8484;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    appearance: none;
    margin: 0;
  }

  .form__input:focus-visible {
    outline: none;
  }

  .form__input_textarea {
    height: 108px;
    resize: none;
    margin-top: 4px;
  }

  .form__input-error {
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #FF8484;
    position: absolute;
    top: 57px;
    left: 0;
  }

  .form__submit-btn {
    width: 284px;
    height: 36px;
    background: #EEEEEE;
    border-radius: 10px;
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 15px;
    text-align: center;
    letter-spacing: 0.02em;
    color: #B4B4B4;
    border: none;
    transition: all 0.5s ease-in-out;
  }

  .form__submit-btn_active {
    cursor: pointer;
    background: #7BAE73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    color: #FFFFFF;
    transition: all 0.5s ease-in-out;
  }

  .form__submit-btn_active:hover {
    opacity: 0.7;
    transition: all 0.5s ease-in-out;
  }
</style>
