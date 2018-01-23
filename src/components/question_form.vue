<template>
    <div class="question_form">

        <!-- Heading -->
        <h1 class="title is-3">Enter the information here</h1>

        <!-- Goal -->
        <h1 class="title is-4">Enter the starting number:</h1>
        <div class="field has-addons">
            <p class="control">
                <a class="button is-static">
                    Starting Number
                </a>
            </p>
            <p class="control">
                <input class="input" type="number" v-model="start_number">
            </p>
        </div>

        <!-- Goal -->
        <h1 class="title is-4">Enter the goal:</h1>
        <div class="field has-addons">
            <p class="control">
                <a class="button is-static">
                    Goal
                </a>
            </p>
            <p class="control">
                <input class="input" type="number" v-model="goal">
            </p>
        </div>

        <!-- Moves -->
        <h1 class="title is-4">Enter the amount of moves you have:</h1>
        <div class="field has-addons">
            <p class="control">
                <a class="button is-static">
                    Moves
                </a>
            </p>
            <p class="control">
                <input class="input" type="number" v-model="moves">
            </p>
        </div>

        <!-- Operations -->
        <h1 class="title is-4">Enter the correct operations available:</h1>
        <nav class="panel">
            <a class="panel-block" v-for="operation in operations">
                <div class="field has-addons" >
                    <div class="control">
                        <a class="button">
                            Type
                        </a>
                    </div>
                    <div class="control">
                        <div class="select">
                            <select v-model="operation.type">
                                <option>Select a type</option>
                                <option>Add</option>
                                <option>Subtract</option>
                                <option>Multiply</option>
                                <option>Divide</option>
                                <option>Delete a digit</option>
                                <option>Flip the sign (+/-)</option>
                                <option>Insert a digit</option>
                                <option>Convert digits</option>
                                <option>Sum the digits</option>
                                <option>Mirror the digits</option>
                            </select>
                        </div>
                    </div>

                    <!-- Add/Sub/Mult/Div/Ins -->
                    <div class="control" v-show="operation.type == 'Add' || operation.type == 'Subtract' || operation.type == 'Multiply' || operation.type == 'Divide' || operation.type == 'Insert a digit'">
                        <a class="button">
                            Value
                        </a>
                    </div>
                    <div class="control" v-show="operation.type == 'Add' || operation.type == 'Subtract' || operation.type == 'Multiply' || operation.type == 'Divide' || operation.type == 'Insert a digit'">
                        <input class="input" type="number" v-model="operation.number">
                    </div>

                    <!-- Convert -->
                    <div class="control" v-show="operation.type == 'Convert digits'">
                        <a class="button">
                            Initial Number
                        </a>
                    </div>
                    <div class="control" v-show="operation.type == 'Convert digits'">
                        <input class="input" type="number" v-model="operation.initial_number">
                    </div>
                    <div class="control" v-show="operation.type == 'Convert digits'">
                        <a class="button">
                            Output Number
                        </a>
                    </div>
                    <div class="control" v-show="operation.type == 'Convert digits'">
                        <input class="input" type="number" v-model="operation.output_number">
                    </div>

                    <!-- Delete -->
                    <p class="control">
                        <a class="button is-danger" v-on:click="removeOperation(operation)">
                            <span class="fa fa-times"></span>
                        </a>
                    </p>
                </div>
            </a>
            <a class="panel-block">
                <a href="#" v-on:click="addOperation">
                    <div class="field has-addons">
                        <div class="control">
                            <a class="button is-primary">
                                Add an operation
                            </a>
                        </div>
                    </div>
                </a>
            </a>
        </nav>
    </div>
</template>

<script>
export default {

    data () {
        return {

        }
    },

    props: ['start_number', 'goal', 'moves', 'operations'],

    methods: {
        addOperation: function(){
            this.operations.push(
                {
                    type: 'Select a type',
                    number: 0,
                    initial_number: 0,
                    output_number: 0,
                    string: '',
                }
            )
        },

        removeOperation: function(operation){
            var index = this.operations.indexOf(operation);

            if (index > -1) {
                this.operations.splice(index, 1);
            }
        },
    },

    watch: {

        start_number: function(){
            this.$emit('start_number', this.start_number)
        },

        goal: function(){
            this.$emit('goal', this.goal)
        },

        moves: function(){
            this.$emit('moves', this.moves)
        },

        operations: function(){
            this.$emit('operations', this.operations)
        }
    }

}
</script>

<style scoped>
    ul{
        list-style: none;
    }
    a{
        text-decoration: none;
    }
</style>
