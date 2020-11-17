<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Представьтесь</span>
        <input
            v-model.trim="name"
            @focus="handleFocus"
            :class="{'is-invalid': error.name}"
            type="text"
            class="form-control"
            name="name"
        />
        <span class="invalid-feedback">{{ error.name }}</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Адрес доставки</span>
        <input
            v-model.trim="address"
            @focus="handleFocus"
            :class="{'is-invalid': error.address}"
            type="text"
            class="form-control"
            name="address"
        />
        <span class="invalid-feedback">{{ error.address }}</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Телефон</span>
        <input
            v-model.trim="phone"
            @focus="handleFocus"
            :class="{'is-invalid': error.phone}"
            type="tel"
            class="form-control"
            name="phone"
            placeholder="+xxxxxxxxxxx"
        />
        <span class="invalid-feedback">{{ error.phone }}</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Эл. почта</span>
        <input
            v-model.trim="email"
            @focus="handleFocus"
            :class="{'is-invalid': error.email}"
            type="email"
            class="form-control"
            name="email"
        />
        <span class="invalid-feedback">{{ error.email }}</span>
      </label>
    </div>
    <div class="form-group">
      <label class="d-block">
        <span class="mb-2">Комментарий</span>
        <textarea
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
      error: {
        name: "",
        address: "",
        phone: "",
        email: "",
      }
    };
  },
  methods: {
    handleFocus({ target }) {
      if (this.error[target.name]) {
        this.error[target.name] = "";
      }
    },

    handleError(data) {
      const { request } = data.error;
      // console.log("handleError -> request", request);

      for (const key in request) {
        // eslint-disable-next-line
        if (request.hasOwnProperty(key)) {
          if (this.error[key] !== undefined) {
            this.error[key] = request[key];
          }
        }
      }
    },

    async post() {
      try {
        const data = {
          name: this.name,
          address: this.address,
          phone: this.phone,
          email: this.email,
          comment: this.comment
        };

        const res = await axios.get(
            "https://vue-study.dev.creonit.ru/api/users/accessKey"
        );
        const userAccessKey = res.data.accessKey;

        await axios.post(
            "https://vue-study.dev.creonit.ru/api/baskets/products",
            {
              "productId": "7",
              "quantity": "10"
            },
            { params: { userAccessKey } });

        // Если запрос идет последним, то зачем ждать?
        // Понятно, что если будет усложняться, то стоит добавить "await".
        // Но в данном случае получается что добавляем навсякий 🤷🏻‍♂️
        await axios
            .post(
                `https://vue-study.dev.creonit.ru/api/orders`,
                data,
                { params: { userAccessKey } }
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
