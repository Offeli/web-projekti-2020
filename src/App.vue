<template>
  <div id="app" class="small-container">
    <h1>Game reviews for kids</h1>
    <button @click="swapCtr">Review Crash team racing</button>
    <p/>
    <button @click="swapHalo">Review Halo 2</button>
    <p/>
    <button @click="swapCiv">Review Civilization 6</button>
    <p/>
    <span v-if="ctrSeen && games.ctrReviews !== 'undefined'">
      <AddingForm @add:ctrReview="addctrReview" />
    </span>
    <span v-if="haloSeen && games.haloReviews !== 'undefined'">
      <AddingForm @add:haloReview="addhaloReview" />
    </span>
    <span v-if="civSeen && games.civReviews !== 'undefined'">
      <AddingForm @add:civReview="addcivReview" />
    </span>
    <GameTable
            :games="games"
            :civReviews="civReviews"
            :ctrReviews="ctrReviews"
            :haloReviews="haloReviews"
    />
  </div>
</template>

<script>
  import GameTable from '@/components/GameTable.vue'
  import AddingForm from '@/components/AddingForm.vue'

  export default {
    name: 'app',
    components: {
      GameTable,
      AddingForm,
    },
    data() {
      return {
        games: [
          {
            id: 1,
            name: 'Crash team racing',

          },
          {
            id: 2,
            name: 'Halo 2',

          },
          {
            id: 3,
            name: 'Civilization 6',

          },
        ],
        civReviews: [
          {
            id: 1,
            comment: 'Hieno peli, mutta ei ihan niin hyvä kun pelisarjan edellinen osa',
            age: '12',
            score: '4'
          },
        ],
        haloReviews: [
          {
            id: 1,
            comment: 'Yksi kaikkien aikojen FPS peleistä!',
            age: '10',
            score: '5'
          },
        ],
        ctrReviews: [
          {
            id: 1,
            comment: 'Lapsuuden paras peli',
            age: '5',
            score: '5'
          },
          {
            id: 2,
            comment: 'Erinomainen peli perheen pienimmille',
            age: '3',
            score: '5'
          },
        ],
        ctrSeen: false,
        haloSeen: false,
        civSeen: false,
      }
    },
    methods: {
      addhaloReview(review) {
        if (this.haloSeen === false){
          return
        }
        const lasthaloId =
                this.haloReviews.length > 0
                        ? this.haloReviews[this.haloReviews.length - 1].id
                        : 0;
        const haloId = lasthaloId + 1;
        const newhaloReview = { ...review, haloId };

        this.haloReviews = [...this.haloReviews, newhaloReview];
      },
      addctrReview(review) {
        if (this.ctrSeen === false){
          return
        }
        const lastctrId =
                this.ctrReviews.length > 0
                        ? this.ctrReviews[this.ctrReviews.length - 1].id
                        : 0;
        const ctrId = lastctrId + 1;
        const newctrReview = { ...review, ctrId };

        this.ctrReviews = [...this.ctrReviews, newctrReview];
      },
      addcivReview(review) {
        if (this.civSeen === false){
          return
        }
        const lastcivId =
                this.civReviews.length > 0
                        ? this.civReviews[this.civReviews.length - 1].id
                        : 0;
        const civId = lastcivId + 1;
        const newcivReview = { ...review, civId };

        this.civReviews = [...this.civReviews, newcivReview];
      },
      swapCtr: function(){
        if (this.ctrSeen === true){
          this.ctrSeen = false
        } else if (this.ctrSeen === false){
          this.ctrSeen = true;
          this.haloSeen = false;
          this.civSeen = false
        }
      },
      swapHalo: function(){
        if (this.haloSeen === true){
          this.haloSeen = false
        } else if (this.haloSeen === false){
          this.ctrSeen = false;
          this.haloSeen = true;
          this.civSeen = false
        }
      },
      swapCiv: function(){
        if (this.civSeen === true){
          this.civSeen = false
        } else if (this.civSeen === false){
          this.ctrSeen = false;
          this.haloSeen = false;
          this.civSeen = true
        }
      }
    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
    margin-left: 1rem;
    font-weight: bold;
  }

  .small-container {
    max-width: 680px;
  }
</style>