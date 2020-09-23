<template>
    <div>
        <b-carousel fade class="carousel" :interval="6000">      
            <div class="time-date">{{ currentDate }}</div>    
            <b-carousel-slide img-src="https://i.imgur.com/NDyHNBy.jpg"></b-carousel-slide>
            <b-carousel-slide img-src="https://i.imgur.com/bW0FzKF.jpg"></b-carousel-slide>
            <b-carousel-slide img-src="https://i.imgur.com/Us4nvWc.jpg"></b-carousel-slide>
            <b-carousel-slide img-src="https://i.imgur.com/VwIgF9m.jpg"></b-carousel-slide>
        </b-carousel>
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentDate: ""
        }
    },
     methods:{
        getCurrentDate() {
            this.currentDate = new Date().toLocaleString();
            let formatDate = this.currentDate.replace(","," - ");
            this.currentDate = formatDate;
        }
    },
    mounted () {
      setInterval(this.getCurrentDate, 500);
    }
}
</script>

<style scoped>
.carousel {
    max-width: 310px;
    min-width: 300px;
}
.carousel, .slide, .carousel-item img {
  border-radius: 12px 12px 6px 6px;
  overflow: hidden;
}

.time-date {
    position: absolute;
    color: #f7f1e3;
    font-family: 'Tomorrow', sans-serif;
    font-size: 0.7rem;
    font-weight: 550;
    z-index: 2;
    bottom: 5px;
    left: 5px;
}
</style>