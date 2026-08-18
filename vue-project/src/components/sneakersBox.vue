<template>
    <div class="card">
        <div class="sneaker-box">
            <div class="foto-section">
                <img :src="foto" alt="Фото кроссовка" class="foto-card" />
            </div>
            <h3>{{ title }}</h3>
            <p>Категория: {{ category }}</p>
            <p>Цена: {{ price.toLocaleString('ru-RU') }}₽</p>
            <button class="add-basket" @click="$emit('add-basket-product', id)" >Добавить в корзину 🛒</button>
        </div>
    </div>
</template>

<script>
    export default{
        props:{
            id: Number,
            title: String,
            category: String,
            price: Number,
            imageUrl: String,
            isFavorite: Boolean,
            isAdded: Boolean,
            count: Number,
            foto: String,
        }
    }
</script>

<style>
    @font-face {
        font-family: 'PlusJakartaSans';
        src: url(../fonts/PlusJakartaSans-Regular.ttf) format('truetype');
        font-weight: 400;
        font-style: normal;
    }
    .card{
        display: inline-block;
        background-color: #1F232D; 
        border: 1px solid rgba(255, 255, 255, 0.12);
        border-radius: 16px;
        padding: 20px;
        text-align: left;
        font-family: 'PlusJakartaSans', sans-serif;
    }

    .foto-card{
        position: relative;
        width: 100%;
        transition: transform 0.3s ease;
    }

    .foto-card:hover{
        transform: scale(1.3);
    }

    .add-basket{
        background-color: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.15);
        border-radius: 8px;
        padding: 10px;
        cursor: pointer;
        transition: background-color 0.2s ease;
    }

    .add-basket:hover{
        background-color: #12141a;
        
    }
</style>