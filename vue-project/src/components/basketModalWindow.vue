<template>
    <Teleport to="body">
        <div class="modal-win">
            <h2>Корзина</h2>
            <div >
                <p>Название: {{ title }}</p>
                <p>Цена: {{ price }}</p>
            </div>
        </div>
    </Teleport>
</template>

<script>
    export default{
        props: {
            isAdded: Boolean,
            title: String,
            price: Number
        }
    }
</script>

<style>
    .modal-win{
        position: fixed; 
        text-align: center;
        border: 1px solid white;
        bottom: 67px;
        right: 55px;
        z-index: 900;
        width: 25%;
        height: 60vh;
        background: #1F232D;
        border-radius: 22px;
    }
</style>