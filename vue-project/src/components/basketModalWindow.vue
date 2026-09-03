<template>
    <Teleport to="body">
        <div class="modal-win">
            <h2>Корзина</h2>
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
        bottom: 30px;
        right: 15px;
        z-index: 900;
        width: 20%;
        height: 70vh;
        background: #1F232D;
        border-radius: 22px;
    }
</style>