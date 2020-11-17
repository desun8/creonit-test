<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Представьтесь</span>
        <input
            ref="name"
            v-model.trim="name"
            @focus="handleFocus"
            type="text"
            class="form-control"
        />
        <span class="invalid-feedback">Ошибка</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Адрес доставки</span>
        <input
            ref="address"
            v-model.trim="address"
            @focus="handleFocus"
            type="text"
            class="form-control"
        />
        <span class="invalid-feedback">Ошибка</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Телефон</span>
        <input
            ref="phone"
            v-model.trim="phone"
            @focus="handleFocus"
            type="tel"
            class="form-control"
        />
        <span class="invalid-feedback">Ошибка</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Эл. почта</span>
        <input
            ref="email"
            v-model.trim="email"
            @focus="handleFocus"
            type="email"
            class="form-control"
        />
        <span class="invalid-feedback">Ошибка</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Комментарий</span>
        <textarea
            ref="comment"
            v-model.trim="comment"
            class="form-control"
        ></textarea>
      </label>
    </div>
    <button type="submit" class="btn btn-primary">Отправить</button>
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "Form",
  data() {
    return {
      name: "",
      address: "",
      phone: "",
      email: "",
      comment: "",
    };
  },
  methods: {
    toggleError(elm, add = false) {
      if (elm === undefined || elm === null) return;

      const ERR_CLASS = "is-invalid";

      if (add) {
        elm.classList.add(ERR_CLASS);
      } else {
        elm.classList.remove(ERR_CLASS);
      }
    },

    handleFocus({ target }) {
      this.toggleError(target, false);
    },

    handleError(data) {
      const { request } = data.error;
      // console.log("handleError -> request", request);

      for (const key in request) {
        // eslint-disable-next-line
        if (request.hasOwnProperty(key)) {
          const elm = this.$refs[key];
          this.toggleError(elm, true);
        }
      }
    },

    async post() {
      try {
        const { name, address, phone, email, comment } = this;
        const data = { name, address, phone, email, comment };

        const res = await axios.get(
            "https://vue-study.dev.creonit.ru/api/users/accessKey"
        );
        const userAccessKey = res.data.accessKey;

        axios
            .post(
                `https://vue-study.dev.creonit.ru/api/orders?userAccessKey=${userAccessKey}`,
                data
            )
            .catch((error) => {
              // console.error("post -> error 🤷🏻‍♂️", error);
              if (error.response) {
                const { data } = error.response;
                this.handleError(data);
              }
            });
      } catch (error) {
        console.error(`Ошибка 🤷🏻‍♂️ ${error}`);
      }
    },
    handleSubmit() {
      console.log("Отправка формы 🐼");
      this.post();
    },
  },
};
</script>

<style scoped>
label > span:not(.invalid-feedback) {
  display: block;
}
</style>
