<template>

    <div id="user-name" v-if="!user.status">
        <p>Пожалуйста введите ваше имя</p>
        <input v-model="user.name" v-on:keyup.13="user.status = true" autofocus maxlength="30">
        <div class="user-name-submit" v-if="user.name && !user.status" v-on:click="user.status = true">OK</div>

        <!--<pre style="font-size: 12px;">{{ $data | json }}</pre>-->
    </div>

    <header v-if="user.status">
        <div class="logo"></div>
        <div class="current-user">Вы зашли как: {{ user.name }}</div>
        <div class="total-order"><a href="#">Посмореть общий заказ</a></div>
    </header>

    <div class="main-content">
        <div v-for="product in items" v-bind:id="product.id" class="product" v-bind:style="{ 'background-image': 'url(' + product.img + ')'}" v-on:click="toggleActive(product)">
            <div class="product-success" @click="$event.target.classList.toggle('product-success-active')"></div>
            <div class="product-description">
                <h4>{{ product.name }}</h4>
                <!--<p class="description">{{ product.description }}</p>-->
            </div>
            <div class="product-price">{{ product.price | currency}}</div>
        </div>
        <div class="total-order">
            <p>Общая сумма заказа: {{  total() | currency }}</p>
        </div>

    </div>

</template>

<script>

    Vue.filter('currency', function (value) {
        return value.toFixed(2) + " ₽";
    });

    new Vue({
        el: "#app",
        data: {
            user:
                {
                    name: "",
                    status: false
                },
            items: [
                {
                    name: "Первое блюдо",
                    price: 130,
                    id: "q10",
                    img: "img/item-1.jpg",
                    active: false
                },
                {
                    name: "Второе блюдо",
                    price: 110,
                    id: "q11",
                    img: "img/item-2.jpg",
                    active: false
                },
                {
                    name: "Салат",
                    price: 65,
                    id: "q12",
                    img: "img/item-3.jpg",
                    active: false
                },
                {
                    name: "Бутерброд",
                    price: 70,
                    id: "q13",
                    img: "img/item-4.jpg",
                    active: false
                },
                {
                    name: "Лимонад",
                    price: 50,
                    id: "q14",
                    img: "img/item-5.jpg",
                    active: false
                },
                {
                    name: "Чай",
                    price: 20,
                    id: "q15",
                    img: "img/item-6.jpg",
                    active: false
                },
                {
                    name: "Десерт",
                    price: 75,
                    id: "q16",
                    img: "img/item-7.jpg",
                    active: false
                },
                {
                    name: "Хлеб",
                    price: 5,
                    id: "q17",
                    img: "img/item-8.jpg",
                    active: false
                },
                {
                    name: "Приборы",
                    price: 10,
                    id: "q18",
                    img: "img/item-9.jpg",
                    active: false
                }
            ]
        },
        methods: {
            toggleActive: function(s){
                s.active = !s.active;
            },
            total: function(){

                var total = 0;

                this.items.forEach(function(s){
                    if (s.active){
                        total+= s.price;
                    }
                });
                return total;
            }
        }
    })
</script>