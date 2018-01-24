<template>
    <div class="operation_input">

        <div class="columns">
            <div class="column is-two-thirds">
                <question_form
                v-bind:start_number="start_number"
                v-bind:moves="moves"
                v-bind:goal="goal"
                v-bind:operations="operations"

                v-on:start_number="setStartNumber"
                v-on:moves="setMoves"
                v-on:goal="setGoal"
                v-on:operations="setOperations">
              </question_form>
            </div>

            <div class="column">
                <solutions
                v-bind:start_number="start_number"
                v-bind:moves="moves"
                v-bind:goal="goal"
                v-bind:operations="operations">
                </solutions>
            </div>
        </div>
    </div>
</template>

<script>

    import question_form from './question_form'
    import solutions from './solutions'

    export default {
        components: {
            question_form,
            solutions
        },

        data () {
            return {

                start_number: 0,

                goal: 0,

                moves: 3,

                operations: [
                    {
                        type: 'Select a type',
                        number: 0,
                        initial_number: 0,
                        output_number: 0,
                        string: '',
                    },
                ],

                solution: '',
            }
          },

        methods: {

            setStartNumber: function(val){
                this.start_number = val
            },

            setGoal: function(val){
                this.goal = val
            },

            setMoves: function(val){
                this.moves = val
            },

            setOperations: function(val){
                this.operations = val
            }

        },
    }
</script>

<style scoped>
    ul{
        list-style: none;
    }
    a{
        text-decoration: none;
    }
    .button-disabled {
        opacity: 0.6;
        pointer-events: none;
    }
</style>
