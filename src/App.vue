<template>
  <main>
    <section>
      <h1>Входное тестовое</h1>
      <p>
        Входное тестовое нужно, чтобы мы понимали твой уровень JavaScript и Vue,
        умение работать с REST API.
      </p>
      <p>
        На проекте подключен Bootstrap, чтобы сэкономить ваше время на вёрстку.
      </p>
      <ul>
        <li>
          API документация:
          <a target="_blank" href="https://vue-study.dev.creonit.ru/"
          >https://vue-study.dev.creonit.ru/</a
          >
        </li>
        <li>
          Bootstrap:
          <a
              href="https://getbootstrap.com/docs/4.5/getting-started/introduction/"
          >https://getbootstrap.com/docs/4.5/getting-started/introduction/</a
          >
        </li>
        <li>
          Vue документация:
          <a href="https://vuejs.org/v2/guide/">https://vuejs.org/v2/guide/</a>
          <br/>
          Вам понадобиться v-model, v-for, v-bind, рендер хуки.
        </li>
      </ul>

      <p>Что будет учитываться при оценке:</p>
      <ol>
        <li>Чистота кода.</li>
        <li>Использование фич Vue.</li>
        <li>Компонентный подход.</li>
        <li>Использование ES6.</li>
      </ol>
    </section>

    <div class="alert alert-secondary" role="alert">
      Вы получили вёрстку, которую вам надо интегрировать с бэком.
    </div>

    <section class="container mb-5">
      <h2>Первое задание</h2>
      <p>Нужно отправить форму Оформления заказа на сервер.</p>
      <p>
        /api/orders:
        <a target="_blank" href="https://vue-study.dev.creonit.ru/#/Orders/post_api_orders"
        >https://vue-study.dev.creonit.ru/#/Orders/post_api_orders</a>
      </p>
      <h3>Требования:</h3>
      <ol>
        <li>
          Сбор данных в форме должен быть реализован на Vue. На всякий случай
          уточняю :-)
        </li>
        <li>
          Обработка ошибок по полям. Ошибки будут приходить в ответе, если вдруг
          поля невалидные.
        </li>
      </ol>
      <h3>Уточнения</h3>
      <ol>
        <li>
          Чтобы полностью отправить форму, нужно перед этим запросить
          пользовательский ключ `/api/users/accessKey`.
        </li>
        <li>
          Форма до конца не отправиться с новым ключом, потому что тогда корзина
          будет пустая. Если вы дошли до этого — считайте что задание готово ;-)
        </li>
      </ol>
      <h4>Оценка менеджера</h4>
      <p>~20 минут. Если незнакомы с Vue — 40 минут.</p>

      <Form/>
    </section>

    <section class="container mb-5">
      <h2>Второе задание</h2>
      <p>
        Нужно доделать вывод товаров. Кто-то начал задачу, а вас попросили
        закончить начатое.
      </p>
      <p>Вывести товары нужно из категории с `id: 3`</p>
      <p>
        /api/products:
        <a target="_blank" href="https://vue-study.dev.creonit.ru/#/Products/get_api_products"
        >https://vue-study.dev.creonit.ru/#/Products/get_api_products</a>
      </p>
      <h3>Требования:</h3>
      <ol>
        <li>Формат продукта должен соответствовать типу `Product`.</li>
      </ol>
      <h4>Оценка менеджера</h4>
      <p>~10 минут. Если незнакомы с Vue — 20 минут.</p>
      <h4>Дополнительное задание</h4>
      <p>
        Зарефакторить карточку товара используя БЭМ наименование. Это ещё займёт
        10 минут.
      </p>

      <ProductsList/>
    </section>
  </main>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";

import Form from "./Form.vue";
import ProductsList from "@/Products/ProductsList";

export default {
  name: "App",
  components: {
    Form,
    ProductsList,
  },
};
</script>
