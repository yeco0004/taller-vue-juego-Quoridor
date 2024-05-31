    <template>
        <div class="quoridor__cell" @click="$emit('click')">
        <player v-if="isPlayer1" :color="player1Color" />
        <player v-if="isPlayer2" :color="player2Color" />
        <obstacle v-if="isObstacle" />
        </div>
    </template>
    
    <script>
    import Player from '../atoms/Player.vue';
    import Obstacle from '../atoms/Obstacle.vue';
    
    export default {
        components: {
        Player,
        Obstacle
        },
        props: {
        x: Number,
        y: Number,
        isPlayer1: Boolean,
        isPlayer2: Boolean,
        isObstacle: Boolean
        },
        computed: {
        player1Color() {
            return 'var(--player1-color)';
        },
        player2Color() {
            return 'var(--player2-color)';
        }
        }
    }
    </script>
    
    <style scoped>
    .quoridor__cell {
        width: 50px;
        height: 50px;
        border: 1px solid var(--border-color);
        position: relative;
        background-color: #fff;
        cursor: pointer;
        transition: background-color 0.3s;
    }
    
    .quoridor__cell:hover {
        background-color: #f0f0f0;
    }
    </style>
    