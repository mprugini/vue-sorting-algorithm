<template>
  <div id="app">
    <Header />
    <button class="btn btn-primary" @click="shuffle(numberArray)">Shuffle!</button>
    <button class="btn btn-primary mx-2" @click="bubbleSort(numberArray)">Bubble Sort</button>
    <button class="btn btn-primary mx-2" @click="selectionSort(numberArray)">Selection Sort</button>
    <button class="btn btn-primary mx-2" @click="insertionSort(numberArray)">Insertion Sort</button>
    <br>
    <br>
    <ul class="list-group list-group-horizontal justify-content-center">
      <li :class="[ number % 2 === 0 ? 'list-group-item list-group-item-primary' : 'list-group-item list-group-item-success' ]" v-for="number in numberArray" :key="number">{{ number }}</li>
    </ul>
  </div>
</template>

<script>
import Header from './components/Header';

export default {
  name: 'App',
  components: {
    Header
  },
  data() {
    return {
      numberArray: [1, 2, 3, 4, 5, 6, 7, 8],
      shuffledArray: []
    }
  },
  methods: {
    arraySetWithoutIndexes(array, index, value) {
      array.splice(index, 1, value);
    },

    arraySwap(array, indexA, indexB) {
      var x = array[indexA];
      this.arraySetWithoutIndexes(array, indexA, array[indexB]);
      this.arraySetWithoutIndexes(array, indexB, x);
    },

    async shuffle(a) {
      var j, i;
      for (i = a.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        this.arraySwap(a, i, j);
      }
    },

    async bubbleSort(a) {
      var len = a.length;
      for (var i = len - 1; i >= 0; i--) {
        for (var j = 1; j <= i; j++) {
          if (a[j - 1] > a[j]) {
            this.arraySwap(a, j - 1, j);
          }
        }
      }
    },

    async selectionSort(a) {
      let i, j;
      for (j = 0; j < a.length - 1; j++) {
        let iMin = j;
        for (i = j + 1; i < a.length; i++) {
          if (a[i] < a[iMin]) {
            iMin = i;
          }
        }
        if (iMin != j) {
          this.arraySwap(a, j, iMin);
        }
      }
    },

    async insertionSort(a) {
      let i, j;
      for (i = 1; i < a.length; i++) {
        j = i;
        while (j > 0 && a[j-1] > a[j]) {
          this.arraySwap(a, j, j-1);
          j--;
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
