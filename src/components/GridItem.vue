<template lang="html">
  
  <div class="grid-item" :class="['grid-item--' + position]">
      <h2>{{ id }}</h2>

      <button @click="changeChildPosition('top')" class="grid-item__btn grid-item__btn--top"></button>
      <button @click="changeChildPosition('right')" class="grid-item__btn grid-item__btn--right"></button>
      <button @click="changeChildPosition('bottom')" class="grid-item__btn grid-item__btn--bottom"></button>
      <button @click="changeChildPosition('left')" class="grid-item__btn grid-item__btn--left"></button>
  </div>
    
</template>

<script lang="js">
    
  export default  {
    name: 'grid-item',
    props: {
        id: {
            type: Number,
            required: true
        },
        emptyTile: {
            type: Number,
            required: true
        },
        position: {
            type: Number,
            required: true
        },
    },
    data() {
      return {
      }
    },
    methods: {     
        changeChildPosition(direction) {
            this.$emit('changePosition', {index: this.id, direction: direction, lastPos: this.position})                                 
        }        
    },
  };
</script>

<style lang="scss">
.grid-item {
  position: relative;
  border: 0.5px solid #f0f0f0;
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
  align-items: center;

  &__btn {
    position: absolute;
    padding: 0;
    width: 35px;
    height: 35px;
    border: none;
    background-color: transparent;
    background-image: url("../assets/arrow.svg");
    background-size: contain;
    background-repeat: no-repeat;
    cursor: pointer;
    outline: none;

    &--left {
      left: 0;
      top: 50%;
      transform: translateY(-50%) rotate(180deg);
    }

    &--right {
      right: 0;
      top: 50%;
      transform: translateY(-50%);
    }

    &--top {
      top: 0;
      left: 50%;
      transform: translateX(-50%) rotate(-90deg);
    }

    &--bottom {
      bottom: 0;
      left: 50%;
      transform: translateX(-50%) rotate(90deg);
    }
  }

  &--1 {
    grid-area: grid-item-1;
  }

  &--2 {
    grid-area: grid-item-2;
  }

  &--3 {
    grid-area: grid-item-3;
  }

  &--4 {
    grid-area: grid-item-4;
  }

  &--5 {
    grid-area: grid-item-5;
  }

  &--6 {
    grid-area: grid-item-6;
  }

  &--7 {
    grid-area: grid-item-7;
  }

  &--8 {
    grid-area: grid-item-8;
  }

  &--9 {
    grid-area: grid-item-9;
  }

  h2 {
    color: #adadad;
    font-family: "Montserrat", sans-serif;
    font-size: 6vw;
    opacity: 0.4;
  }
}
</style>