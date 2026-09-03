<template>
  <div class="all-magazine">
    <header class="header-magazine">
      <h2>NEO-KICKS</h2>
      <nav>
        <ol class="header-category">
          <li><a class="header-nav" href="" @click.prevent>О НАС</a></li>
          <li><a class="header-nav" href="" @click.prevent>ТОВАРЫ</a></li>
          <li><a class="header-nav" href="" @click.prevent>ОТЗЫВЫ</a></li>
        </ol>
        <button class="btn-nav">Menu</button>
      </nav>
    </header>
    <div class="input-sneaker">
      <input v-model="inputText" class="text-input" type="text" placeholder="Введите название"/>
      <div class="select-category-box">
        <select class="select-category" v-model="selctedCategory">
          <option class="select-option-category" selected>Все</option>
          <option class="select-option-category" >Nike</option>
          <option class="select-option-category">Adidas</option>
          <option class="select-option-category">New Balance</option>
        </select>
      </div>
    </div>
    <div class="check-basket">
      <button @click="openBasket" class="basket">🛒</button>
      <Transition name="fade">
        <p v-show="counterBasket > 0" class="basket-count-box-text">{{ counterBasket }}</p>
      </Transition>
    </div>

    <div class="all-cards">
      <sneakersBox v-for="sneaker in showInputCard" :key="sneaker.id" :title="sneaker.title" :category="sneaker.category" :price="sneaker.price" :foto="sneaker.foto" :count="sneaker.count" :isAdded="sneaker.isAdded" @add-basket-product="addProduct(), visibleButton(), counterSneaker(sneaker.id)"></sneakersBox>
    </div>

    <basketModalWindow v-if="openBask"></basketModalWindow>
  
  </div>
</template>

<script>
  import sneakersBox from './components/sneakersBox.vue';
  import foto1 from './assets/foto1.png';
  import basketModalWindow from './components/basketModalWindow.vue';

  export default{
    components: {sneakersBox, basketModalWindow},
    data(){
      return {
        sneakers: [
          {id: 1, title: "Nike Air Max Plus OG", category: "Nike", price: 18990,isFavorite: false,isAdded: false,count: 7, foto: foto1},
          {id: 2,title: "Adidas Originals Forum Low",category: "Adidas",price: 13490,isFavorite: false,isAdded: false,count: 4, foto: foto1},
          {id: 3,title: "Air Jordan 1 Retro High OG",category: "Jordan",price: 22990,isFavorite: false,isAdded: false,count: 2, foto: foto1},
          {id: 4,title: "New Balance 1906R Cyber",category: "New Balance",price: 19490,isFavorite: false,isAdded: false,count: 5, foto: foto1},
          {id: 5,title: "Nike Dunk Low Retro",category: "Nike", price: 14990,isFavorite: false,isAdded: false,count: 3, foto: foto1},
          {id: 6,title: "Adidas Yeezy Boost 350 V2",category: "Adidas",price: 27990,isFavorite: false,isAdded: false,count: 1, foto: foto1},
          {id: 7,title: "Air Jordan 4 Retro Metallic",category: "Jordan",price: 25490,isFavorite: false,isAdded: false,count: 4, foto: foto1},
          {id: 8,title: "New Balance 9060 Dark",category: "New Balance",price: 21990,isFavorite: false,isAdded: false,count: 9, foto: foto1}],

        counterBasket: 0,
        openBask: false,
        isVisible: true,
        inputText: '',
        newInputArr: [],
        selctedCategory: 'Все'
      }
    }, 
    computed: {
       showInputCard(){
        return this.sneakers.filter((sneaker) => {
          const titleFilter = sneaker.title.toLowerCase().includes(this.inputText);

          const categoryFilter = this.selctedCategory === 'Все' || sneaker.category === this.selctedCategory;

          return titleFilter && categoryFilter
        })
      }
    },

    methods: {
      addProduct(){
        return this.counterBasket++;
      },
      visibleButton(){
        this.isVisible = false;
      }, 
      counterSneaker(id){
        const countSneaker = this.sneakers.find(sneaker => sneaker.id === id)
        countSneaker.count--
        if (countSneaker.count === 0){
          countSneaker.count = 'Нет в наличии';
        }
      },
      openBasket(){
        if (this.openBask === false){
          this.openBask = true
          console.log('Видно модальное окно')
        }
        else{
          this.openBask = false
          console.log('Не видно модальное окно')
        }
      }
    }
  }
</script>

<style>
    @font-face {
        font-family: 'PlusJakartaSansBold';
        src: url(../fonts/PlusJakartaSans-Bold.ttf) format('truetype');
        font-weight: 700;
        font-style: normal;
    }

  @font-face {
        font-family: 'PlusJakartaSans';
        src: url(../fonts/PlusJakartaSans-Regular.ttf) format('truetype');
        font-weight: 400;
        font-style: normal;
    }

  *{

    box-sizing: border-box;
    color: white;
  }

  body{
    background-color: #0D0E12;
  }
  .header-nav{
    outline: none;
    text-decoration: none;
  }

  .all-cards{
    position: relative;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 500px));
    justify-content: center;
    justify-items: center;
    align-items: center;
    margin-left: 10vh;
    margin-right: 10vh ;
    gap: 30px;
    z-index: 10;
  }
  .btn-nav{
    display: none;
  }

  .modal-window{
    position: sticky;
    margin-right: 10px;
  }

  .header-magazine{
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin: 20px 40px 15px 20px;
    font-family: 'PlusJakartaSansBold', sans-serif;
  
  }
  .header-category{
    display: flex;
    list-style: none;
    gap: 10px;
    
  }
  .check-basket{
    position: fixed;
    display: flex;
    justify-content: flex-end;
    bottom: 30px;
    right: 5px;
    z-index: 910;
  }

  .basket-count-box-text{
    color: white;
    right: 8px;
    position: absolute;
    border: 1px solid #ec3535;
    border-radius: 50%;
    padding: 1px 6px;
    bottom: 18px;
    background: #ec3535;
  }

  .basket{
    background-color: white;
    border: none;
    margin-right: 10px;
    border-radius: 50%;
    padding: 12px 15px; 
    cursor: pointer;
    transition: transform 0.3s ease;
    transition: background-color 0.3s ease;
    font-size: 17px;
    aspect-ratio: 1 / 1;
  }

  .basket:hover{
    transform: scale(1.15);
    background-color: rgb(194, 191, 191);
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.1s ease;
  }


  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }

  .input-sneaker{
    position: relative;
    display: flex;
    justify-content: center;
   
  }

  .select-category-box {
    position: absolute;
    right: 40px;
  }


  .text-input{
    max-width: 100%;
    color: rgb(255, 255, 255);
    margin-bottom: 30px;
    padding: 10px 40px;
    background-color:#1F232D;
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 8px;
    outline: none;
    text-align: center;
    font-family: 'PlusJakartaSans', sans-serif;
    field-sizing: content;
  }

  .select-option-category{
    color: rgb(255, 255, 255);
  }

  .select-category{
    padding: 10px;
    color: rgb(255, 255, 255);
    height: 10%;
    border-radius: 8px;
    background-color:#1F232D;
    border: 1px solid rgba(255, 255, 255, 0.12);
  }



   @media (max-width: 550px) {
    .all-cards{
      margin-left: 4vh;
      margin-right: 4vh ;
  }
    .btn-nav{
      position: relative;
      display: block;
      color: #0D0E12;
      background: white;
      border-radius: 10px;
      border: none;
      padding: 5px 10px;
      bottom: 6px;
  }
    .header-category{
      display: none;
    }

    .input-sneaker {
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }

    .select-category-box {
      position: static;
      margin-bottom: 20px;
    }

    .text-input {
      margin-bottom: 15px;
    }
  }
</style>