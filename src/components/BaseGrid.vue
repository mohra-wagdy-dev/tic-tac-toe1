<template>
    <div class="container">
      <div class="gameStatus" :class="gameStatusColor">
        {{ gameStatusMessage }}
      </div>
      <div class="grid">
        <BaseCell v-for="n in 9" :key="n" :marker="cells[n]" :cell-number="n" />
      </div>
    </div>
  </template>
  
  <script>
  import EventBus from "../EventBus.js";
  import BaseCell from "./BaseCell.vue";
  
  export default {
    name: "BaseGrid",
    components: {
      BaseCell
    },
    created() {
      EventBus.$on("shot", (cellNumber) => {
        // تحديث الخلية بشكل صحيح باستخدام Vue.set
        this.$set(this.cells, cellNumber, this.activePlayer);
        this.moves++;
        
        // تغيير حالة اللاعب بعد كل حركة
        this.switchPlayer();
        
        // تحقق من الفوز أو التعادل بعد كل حركة (يمكنك إضافة منطق هنا لاحقًا)
        this.checkWin();
      });
    },
    data() {
      return {
        activePlayer: "O",
        gameStatus: "turn",
        gameStatusMessage: "O turn",
        gameStatusColor: "statusTurn",
        moves: 0,
        winCondition: [
          [1, 2, 3], [4, 5, 6], [7, 8, 9],
          [1, 4, 7], [2, 5, 8], [3, 6, 9],
          [1, 5, 9], [3, 5, 7]
        ],
        cells: {
          1: "", 2: "", 3: "",
          4: "", 5: "", 6: "",
          7: "", 8: "", 9: "",
        }
      };
    },
    methods: {
      switchPlayer() {
        this.activePlayer = this.activePlayer === "O" ? "X" : "O";
        this.gameStatusMessage = `${this.activePlayer} turn`;
        this.gameStatusColor = this.activePlayer === "O" ? "statusTurn" : "statusTurn";
      },
      checkWin() {
        // تحقق من فوز أي لاعب بناءً على winCondition
        for (let condition of this.winCondition) {
          const [a, b, c] = condition;
          if (this.cells[a] && this.cells[a] === this.cells[b] && this.cells[a] === this.cells[c]) {
            this.gameStatusMessage = `${this.activePlayer} wins!`;
            this.gameStatusColor = "statusWin";
            return;
          }
        }
        // تحقق من التعادل
        if (this.moves === 9) {
          this.gameStatusMessage = "It's a draw!";
          this.gameStatusColor = "statusDraw";
        }
      }
    }
  };
  </script>
  
  <style lang="css" scoped>
  .grid {
    display: grid;
    grid-template-columns: 120px 120px 120px;
    grid-gap: 10px;
    background-color: darkcyan;
    color: white;
    width: 100%;
    position: relative;
    padding: 10px;
    box-sizing: border-box;
  }
  .gameStatus {
    padding: 20px 0px;
    border-radius: 50%;
    font-size: 2em;
    font-weight: 800;
    color: wheat;
  }
  .statusTurn {
    background-color: gold;
  }
  .statusWin {
    background-color: green;
  }
  .statusDraw {
    background-color: grey;
  }
  </style>
  