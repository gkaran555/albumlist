<template>
  <div id="app" v-cloak>
    <div class="wraper">
      <transition name="slide" mode="out-in">
           <router-view/>
       </transition>
    </div>
    
  </div>
</template>

<style lang="scss">

[v-cloak] {
	display: none !important;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1200px;
  margin: 70px auto; 
  @media only screen and (max-width: 450px) {
    margin: 35px auto;
  }
}

.wraper {
  box-shadow: 0 5px 20px 0 rgba(0,0,0, .25);
}

.slide-enter-active {
  animation: slide-in 200ms ease-out forwards;
}

.slide-leave-active {
  animation: slide-out 200ms ease-out forwards;
}

@keyframes slide-in {
    from {
        transform: translateX(-30px);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

@keyframes slide-out {
    from {
        transform: translateX(0);
        opacity: 1;
    }
    to {
        transform: translateX(-30px);
        opacity: 0;
    }
}

</style>
