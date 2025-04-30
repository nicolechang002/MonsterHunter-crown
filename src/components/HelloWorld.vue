<script setup>
  import {ref, watch} from 'vue';

  // ===魔物資料區===
  const monsters = ref([
    {name:"纏蛙", icon:"Chatacabra.png", big_crown:false, small_crown:false},
    {name:"炎尾龍", icon:"Quematrice.png", big_crown:false, small_crown:false},
    {name:"刺花蜘蛛", icon:"Lala_Barina.png", big_crown:false, small_crown:false},
    {name:"桃毛獸王", icon:"Congalala.png", big_crown:false, small_crown:false},
    {name:"沙海龍", icon:"Balahara.png", big_crown:false, small_crown:false},
    {name:"闢獸", icon:"Doshaguma.png", big_crown:false, small_crown:false},
    {name:"波衣龍", icon:"Uth_Duna.png", big_crown:false, small_crown:false},
    {name:"沼噴龍", icon:"Rompopolo.png", big_crown:false, small_crown:false},
    {name:"煌雷龍", icon:"Rey_Dau.png", big_crown:false, small_crown:false},
    {name:"影蜘蛛", icon:"Nerscylla.png", big_crown:false, small_crown:false},
    {name:"風鋏龍", icon:"Hirabami.png", big_crown:false, small_crown:false},
    {name:"赫猿獸", icon:"Ajarakan.png", big_crown:false, small_crown:false},
    {name:"獄焰鱆", icon:"Nu_Udra.png", big_crown:false, small_crown:false},
    {name:"護闢獸", icon:"Guardian_Doshaguma.png", big_crown:false, small_crown:false},
    {name:"護火龍", icon:"Guardian_Rathalos.png", big_crown:false, small_crown:false},
    {name:"護兇爪龍", icon:"Guardian_Ebony_Odogaron.png", big_crown:false, small_crown:false},
    {name:"暗器鱆", icon:"Xu_Wu.png", big_crown:false, small_crown:false},
    {name:"怪鳥", icon:"Yian_Kut-Ku.png", big_crown:false, small_crown:false},
    {name:"毒怪鳥", icon:"Gypceros.png", big_crown:false, small_crown:false},
    {name:"雌火龍", icon:"Rathian.png", big_crown:false, small_crown:false},
    {name:"護雷顎龍", icon:"Guardian_Fulgur_Anjanath.png", big_crown:false, small_crown:false},
    {name:"火龍", icon:"Rathalos.png", big_crown:false, small_crown:false},
    {name:"鎧龍", icon:"Gravios.png", big_crown:false, small_crown:false},
    {name:"雪獅子王", icon:"Blangonga.png", big_crown:false, small_crown:false},
    {name:"黑蝕龍", icon:"Gore_Magala.png", big_crown:false, small_crown:false},
    {name:"鎖刃龍", icon:"Arkveld.png", big_crown:false, small_crown:false},
    {name:"泡狐龍", icon:"Mizutsune.png", big_crown:false, small_crown:false}
  ])

  // ===初始化區域(localStroage)===
  const monsterData = JSON.parse(localStorage.getItem("monsterData"));
  if(monsterData){
    monsters.value.splice(0, monsters.value.length,...monsterData)
  }

  // ===操作區===
  const saveToLocalStorage = () =>{
    localStorage.setItem("monsterData",JSON.stringify(monsters.value));
  }

  watch(monsters,() => {
    saveToLocalStorage();
  },{deep:true});

  const getImgUrl = (name) =>{
    return new URL(`../icon/${name}`, import.meta.url).href
  }

  const crownChecked = (monster) => {
      if(monster.big_crown && monster.small_crown){
        return "#b76e2d"; //大金小金皆完成
      }
      if(monster.big_crown || monster.small_crown){
          return "#623f2b"; //其中一個完成
        }
      else{
        return "#555151"; //大金小金皆沒完成
      }
  }
</script>

<template>
  <div>
    <h1>魔物獵人大小金</h1>
    <p>請勾選已收集的大小金</p>
    <div class="grid-box">
      <div v-for="monster in monsters" :key="monster.name" class="monster-card" :style="{backgroundColor: crownChecked(monster)}">
        <img :src="getImgUrl(monster.icon)" :alt="monster.name" width="270" height="270"/>
        <p class="monster-card__name">{{ monster.name }}</p>
        <label class="monster-card__checkbox">小金<input type="checkbox" v-model="monster.small_crown"></label>
        <label class="monster-card__checkbox">大金<input type="checkbox" v-model="monster.big_crown"></label>
      </div>
    </div>
  </div>
</template>

<style>
  /* ===全域樣式(Typography)=== */
  h1{
    font-family: Noto Sans TC;
    text-align: center;
  }

  p{
    font-family: Noto Sans TC;
    font-size: 18px;
    text-align: center;
  }

  /* ===主要容器樣式=== */
  .grid-box{
    display: flex;
    flex-wrap: wrap;
    justify-self: center;
    gap: 20px;
  }

  /* ===卡片樣式=== */
  .monster-card{
    font-family: Noto Sans TC;
    flex: 0 0 calc(16% - 1rem);
    box-sizing: border-box;
    background-color:#555151;
    padding: 10px;
    text-align: center;
    border-radius: 10px;
    box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
  }

  .monster-card:hover{
    box-shadow: 3px 3px 5px rgba(255, 255, 255,0.5);
  }

  .monster-card img{
    width: 150px;
    height: 150px;
    border-radius: 5px;
    object-fit: contain;
  }

  .monster-card__checkbox{
    font-family: Noto Sans TC;
    width: 100%;
    text-align: center;
    margin: 0 5px;
    font-size: 18px;
    color:#ffffff;
  }  

  /* ===響應式設計=== */
  @media screen and (max-width:768px) {
    h1{
      font-size: 24px;
    }

    p{
      font-size: 14px;
    }

    .grid-box{
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 0 1rem;
      grid-template-columns: none;
    }

    .monster-card{
      flex: 0 0 calc(50% - 1rem);
      width: auto;
      font-size: 14px;
    }

    .monster-card__checkbox{
      font-size: 14px;
      margin: 0;
    }

    .monster-card img{
      width: 100px;
      height: 100px;
    }

    .monster-card__name{
      font-size: 1.2em;
      font-weight: bold;
    }
    
  }
</style>
