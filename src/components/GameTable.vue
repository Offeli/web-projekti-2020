<template>
<div id="GameTable">
    <table>
        <thead>
        <tr>
            <th>Game name</th>
            <th>Reviews</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="game in games" :key="game.id">
            <td >{{game.name}}</td>
            <td v-if="game.id === 1">
                <button @click="swapCtr">See reviews</button>
                <template v-if="ctrSeen">
                <span v-for="ctrReview in ctrReviews" :key="ctrReview.id" class="reviews">
                    <br>
                    Age recommendation: {{ ctrReview.age }},
                    Score: {{ctrReview.score}},
                    Comment: {{ctrReview.comment}}
                </span>
                </template>
            </td>
            <td v-else-if="game.id === 2">
                <button @click="swapHalo">See reviews</button>
                <template v-if="haloSeen">
                <span v-for="haloReview in haloReviews" :key="haloReview.id"  class="reviews">
                    <br>
                    Age recommendation: {{ haloReview.age }},
                    Score: {{haloReview.score}},
                    Comment: {{haloReview.comment}}
                </span>
                </template>
            </td>
            <td v-else-if="game.id === 3">
                <button @click="swapCiv">See reviews</button>
                <template v-if="civSeen">
                <span v-for="civReview in civReviews" :key="civReview.id"  class="reviews">
                    <br>
                    Age recommendation: {{ civReview.age }},
                    Score: {{civReview.score}},
                    Comment: {{civReview.comment}}
                </span>
                </template>
            </td>
        </tr>
        </tbody>
    </table>

</div>
</template>

<script>
  export default {
    name: 'GameTable',
    props: {
      games: Array,
      ctrReviews: Array,
      haloReviews: Array,
      civReviews: Array
    },
    data() {
      return {
        ctrSeen: false,
        haloSeen: false,
        civSeen: false
      }
    },
    methods: {
      swapCtr: function(){
        if (this.ctrSeen === true){
          this.ctrSeen = false
        } else if (this.ctrSeen === false){
          this.ctrSeen = true
        }
      },
      swapHalo: function(){
        if (this.haloSeen === true){
          this.haloSeen = false
        } else if (this.haloSeen === false){
          this.haloSeen = true
        }
      },
      swapCiv: function(){
        if (this.civSeen === true){
          this.civSeen = false
        } else if (this.civSeen === false){
          this.civSeen = true
        }
      }
    }
  }
</script>

<style scoped>
    button {
        margin: 0 0.5rem 0 0;
    }
</style>