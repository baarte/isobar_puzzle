<template lang="html">
  
  <div class="container">
    <div class="grid-layout">

      <!-- A grid item component that loads every item out of the gridItems array in the data object, gives them props, such as original tile and current position -->
      <grid-item v-for='(gridItem, index) in gridItems' :key='index' :id='gridItem.id' :emptyTile='emptyTile' :position='gridItem.position' @changePosition='changeItemPosition'></grid-item>    
    </div>

    <!-- A button to shuffle the position of the tiles -->
    <button @click='shuffle' class="btn btn--shuffle">Shuffle</button>
  </div>
    
</template>

<script lang="js">
  import GridItem from '@/components/GridItem'
    
  export default  {
    name: 'grid-layout',
    components: {
      GridItem
    },
    data() {
      return {
        // the position of the empty tile at start
        emptyTile: 9,

        // array of tiles
        gridItems: [
          { id: 1,
            position: 1 
          },
          { id: 2,
            position: 2 
          },
          { id: 3,
            position: 3 
          },
          { id: 4,
            position: 4 
          },
          { id: 5,
            position: 5 
          },
          { id: 6,
            position: 6 
          },
          { id: 7,
            position: 7 
          },
          { id: 8,
            position: 8 
          },
        ]
      }
    },
    methods: {
      changeItemPosition(value) {
        let index = value.index-1,
            direction = value.direction,
            lastPos = value.lastPos;

        // based on what direction is clicked move tile, except if there is already another tile
        if(direction === 'top' && this.emptyTile === this.gridItems[index].position-3) {
          this.gridItems[index].position = this.gridItems[index].position-3
          this.emptyTile = lastPos
        } 
        else if(direction === 'left' && this.emptyTile === this.gridItems[index].position-1) {
          this.gridItems[index].position = this.gridItems[index].position-1
          this.emptyTile = lastPos
        }
        else if(direction === 'right' && this.emptyTile === this.gridItems[index].position+1) {
          this.gridItems[index].position = this.gridItems[index].position+1
          this.emptyTile = lastPos
        }
        else if(direction === 'bottom' && this.emptyTile === this.gridItems[index].position+3) {
          this.gridItems[index].position = this.gridItems[index].position+3
          this.emptyTile = lastPos
        }
      },
      shuffle() {
        let i;
        let shuffledTileNumbers = [1,2,3,4,5,6,7,8,9];           

        for (i = 0; i < this.gridItems.length; i++) {          
          // get a random number from the array of tiles, change the position of the tile and remove the number from the area that is already changed.
          let randomValue = shuffledTileNumbers[Math.floor(Math.random() * shuffledTileNumbers.length)],
              arrIndex = shuffledTileNumbers.indexOf(randomValue);  

          this.gridItems[i].position = randomValue;

          shuffledTileNumbers.splice(arrIndex, 1)
        }

        // give the empty tile a new value
        this.emptyTile = shuffledTileNumbers[0]
      }
    },
  };
</script>

<style lang="scss">
.container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.grid-layout {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  grid-template-areas:
    "grid-item-1 grid-item-2 grid-item-3"
    "grid-item-4 grid-item-5 grid-item-6"
    "grid-item-7 grid-item-8 grid-item-9";
  width: 100%;
  height: 100%;
  max-width: 500px;
  max-height: 500px;
}

.btn {
  border: none;
  padding: 15px 25px;
  border-radius: 4px;
  font-size: 15px;
  font-weight: bold;
  text-transform: uppercase;
  cursor: pointer;
  outline: none;

  &--shuffle {
    margin-top: 10px;
    background: #42b883;
    color: #fff;
    transition: 0.2s ease-out;

    &:hover {
      background: #218055;
    }
  }
}
</style>