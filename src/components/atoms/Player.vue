    <template>
        <div :style="{ backgroundColor: color }" class="quoridor__player"></div>
    </template>
    
    <script>
    export default {
        props: {
        color: String
        }
    }
    </script>
    
    <style scoped>
    .quoridor__player {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        position: absolute;
        top: 5px;
        left: 5px;
    }
    </style>
    