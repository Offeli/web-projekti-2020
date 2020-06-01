<template>
    <div id="AddingForm">
        <form @submit.prevent="handleSubmit">
            <p>
                <label> Review: </label>
                <input
                        class="review-area"
                        type="text"
                        :class="{ 'has-error': submitting && invalidComment }"
                        v-model="review.comment"
                        @focus="clearStatus"
                        @keypress="clearStatus"
                />
            </p>

            <p>
                <label> Age suggestion: </label>
                <input
                        type="text"
                        :class="{ 'has-error': submitting && invalidAge }"
                        v-model="review.age"
                        @focus="clearStatus"
                        @keypress="clearStatus"
                />
            </p>

            <p>
                <label > Rating: </label>
                <select id="score" v-model="review.score">
                    <option>5</option>
                    <option>4</option>
                    <option>3</option>
                    <option>2</option>
                    <option>1</option>
                </select>
            </p>

            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                ✅ Review successfully added
            </p>
            <p/>
            <button>Add Review</button>
        </form>
    </div>
</template>

<script>
  export default {
    name: 'AddingForm',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        review: {
          score: ' ',
          age: ' ',
          comment: ' ',
        }
      }
    },
    methods: {
      handleSubmit() {
        this.submitting = true;
        this.clearStatus();

        if (this.invalidComment || this.invalidScore || this.invalidAge) {
          this.error = true;
          return
        }

        this.$emit('add:ctrReview', this.review);
        this.$emit('add:haloReview', this.review);
        this.$emit('add:civReview', this.review);
        this.$refs.first.focus();

        this.review = {
          score: ' ',
          age: ' ',
          comment: ' ',
        };
        this.error = false;
        this.success = true;
        this.submitting = false
      },

      clearStatus() {
        this.success = false;
        this.error = false
      }
    },
    computed: {
      invalidComment() {
        return this.review.comment === ''
      },

      invalidScore() {
        return this.review.score === ''
      },

      invalidAge() {
        return this.review.age === ''
      },
    },
  }
</script>

<style scoped>
    form {
        margin: 1rem;
        border: double;
        padding: 1rem;
    }

    [class*='-message'] {
        font-weight: 500;
    }
    .review-area{
        height: 5rem;
        width: 20rem;
    }
    .error-message {
        color: #d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>