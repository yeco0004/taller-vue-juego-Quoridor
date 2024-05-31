    <template>
        <section class="quoridor__board">
        <section v-for="(row, i) in board" :key="i" class="quoridor__row">
            <board-cell
            v-for="(cell, j) in row"
            :key="j"
            :x="j"
            :y="i"
            :isPlayer1="isPlayer1(i, j)"
            :isPlayer2="isPlayer2(i, j)"
            :isObstacle="isObstacle(i, j)"
            @click="handleClick(i, j)"
            />
        </section>
        </section>
    </template>
    
    <script>
    import BoardCell from './BoardCell.vue';
    
    export default {
        components: {
        BoardCell
        },
        props: {
        board: Array,
        player1: Object,
        player2: Object,
        obstacles: Array
        },
        methods: {
        handleClick(i, j) {
            this.$emit('cell-click', i, j);
        },
        isPlayer1(i, j) {
            return this.player1.x === j && this.player1.y === i;
        },
        isPlayer2(i, j) {
            return this.player2.x === j && this.player2.y === i;
        },
        isObstacle(i, j) {
            return this.obstacles.some(obstacle => obstacle.x === j && obstacle.y === i);
        }
        }
    }
    </script>
    
    <style scoped>
    .quoridor__board {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-bottom: 20px;
    }
    
    .quoridor__row {
        display: flex;
    }
    </style>
    