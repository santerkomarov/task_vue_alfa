<template>
  <div class="container">
    
    <div 
      v-for="(item, key) in items" 
      :key="key" 
      class="block"
    >
      <img :src="item.image" class="block-image"/>
      <div class="block-content">
        <h3>{{ item.name }}</h3>
        <div>
          <div class="block-date">
            <p>{{ item.date.date }}</p>
            <div class="block-date-year">
              <div>
                {{ monthNames[item.date.month] }}
              </div>
              <div>
                {{ item.date.year }}
              </div>
            </div>
          </div>
        </div>
        <div>
          {{ item.previewText }}
        </div>
      </div>  
      <div class="block-value">
        <span class="">{{ item.type.value }}</span>
      </div>
    </div>
  </div>
  <div class="wrap-btn">
    <button 
      v-if="total-current" 
      class="btn" 
      @click="load()"
      >
      Загрузить ещё
    </button>
  </div>
  
</template>

<script>
import axios from 'axios'

export default {
  name: 'FirstPage',
  data() {
      return {
        items: [],      // новости
        current: 0,     // текущая страница
        total: 0,       // всего страниц
        url: "https://flems.github.io/test/api/news/",
        monthNames: [
          "January", 
          "February", 
          "March", 
          "April", 
          "May", 
          "June",
          "July", 
          "August", 
          "September", 
          "October", 
          "November", 
          "December"
        ],
      };
  },
  mounted() {
    this.load();
  },
  methods: {
    // Переводит timestamp в человеческий язык
    convert(arg) {
      return {
        date: new Date(arg * 1000).getDate(),
        month: new Date(arg * 1000).getMonth() + 1,
        year: new Date(arg * 1000).getFullYear()
      }
    },
    load() {
      // параметр запроса, https://flems.github.io/test/api/news/next
      let next = this.current ? this.current + 1 : "";

      axios
        .get(this.url + next)
        .then((response) => {
          this.current = response.data.nav.current;
          this.total = response.data.nav.total;
          response.data.items.map( (item) => {
            // Конвертируем дату
            item.date = this.convert(item.date);
          })
          if (this.items.length) {
            // Загрузки были ? если да то добавляем
            this.items = this.items.concat( response.data.items);
          } else {
            // Первоначальная загрузка
            this.items = response.data.items;
          }
        })
        .catch(function (error) {
          console.log(error.toJSON());
        });
    }
  }

}
</script>

<style scoped>
.container {
  max-width: 1300px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
.block {
  display: flex; 
  flex-direction: 
  column; width:400px; 
  min-height: 300px; 
  flex-wrap: wrap; 
  gap:20px;
  border:1px solid blue;
  border-radius: 10px;
}
.block-image {
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
.block-content {
  border-radius: 10px;
  padding: 10px;
  flex-grow: 1;
}

.block-date {
  display: flex;
  
}
.block-date p {
  font-size: 36px;
  margin: 0;
  padding-right: 10px;
}
.block-date-year {
  display: flex;
  flex-direction: column;
}

.block-value {
  padding: 10px;
}
.block-value span{
  background-color: #ccc;
}

.wrap-btn {
  display: flex;
  justify-content: center;
  padding: 10px;
  margin-bottom: 100px;
}
.btn {
  width: 300px;
  height: 40px;
  background-color: #fff;
  transition: 0.3s;
  cursor: pointer;
}
.btn:hover {
  background-color: #ccc;
}
h3 {
  color: blue;
}
</style>
