<template>
    <div class="solutions">

        <!-- Heading -->
        <h1 class="title is-3">The solutions will show here</h1>
        <button class="button is-primary" v-on:click="find_solutions()">Generate Solutions</button><br><br>

        <div v-show="true">
          <h3>Show all data</h3>
          Start Number: {{ start_number }}<br>
          Goal: {{ goal }}<br>
          Moves: {{ moves }}<br>
          Operations:<br>
          <ul>
            <li v-for="(operation, x) in operations">
              Operation {{ x }}:
              Type: {{ operation.type }}
            </li>
          </ul><br>

          <h3>Test operate()</h3>
          {{ test.value }} --> {{ test.operation.type }}:{{ test.operation.number }} = {{ operate(test.operation, test.value) }}
        </div>

        <!-- Solutions -->
        <nav class="panel">
            <a class="panel-block"  v-for="solution in solutions" v-show="solution.answer == goal">
              <div class="field has-addons">
                <div class="control">
                  <a class="button is-info">
                    {{ start_number }}
                  </a>
                </div>
                <div class="control" v-for="step in solution.arr">
                  <a class="button" >
                      {{ step }}
                  </a>
                </div>

                <div class="control">
                  <a class="button is-info">
                    = {{ solution.answer }}
                  </a>
                </div>
              </div>
            </a>
        </nav>

    </div>
</template>

<script>
export default {
    data () {
        return {
            solutions: [],

            test: {
              operation: {
                type: 'Mirror the digits',
                number: 0,
                initial_number: 0,
                output_number: 0,
                string: '',
              },
              value: 21
            }
        }
    },

    props: ['start_number', 'goal', 'moves', 'operations'],

    methods:{

        find_solutions: function(){

          // clear the solutions array
          this.solutions = []

          // add all possible moves to solution array
          this.solve(this.moves, [])
        },

        solve: function(moves, solOperations){
            if(moves > 0){

              // loop through available operations
              for(var i = 0; i < this.operations.length; i++){

                // decrease moves
                var Moves = moves - 1

                // add operation to solution
                var SolOperations = []
                for(var x = 0; x < solOperations.length; x++){
                  SolOperations.push(solOperations[x])
                }
                SolOperations.push(this.operations[i])

                // recurse
                this.solve(Moves, SolOperations)
              }
            }
            else{
              var result = this.start_number
              for(var i = 0; i < solOperations.length; i++){
                result = this.operate(solOperations[i], result)
              }

              this.solutions.push(this.generate_solution(solOperations, result))
            }
        },

        generate_solution: function(arr, result){

          // create string array
          var str_arr = []
          for(var i = 0; i < arr.length; i++){
            str_arr.push(this.generate_solution_string(arr[i]))
          }

          var solution = {
              arr: str_arr,
              answer: result
          }

          return solution
        },

        operate: function(operation, value){

          /*
            Possible errors:
            - divide by zero
          */

          var output = parseInt(value)

          switch(operation.type){
              case 'Add':
                output = output + parseInt(operation.number)
                break
              case 'Subtract':
                output = output - operation.number
                break
              case 'Multiply':
                output = output * operation.number
                break
              case 'Divide':
                if(operation.number == 0){
                  output = 0
                }
                else{
                  output = output / operation.number
                }
                break
              case 'Delete a digit':
                var str = output.toString().slice(0, -1)
                output = parseInt(str)
                break
              case 'Flip the sign (+/-)':
                output = output * -1
                break
              case 'Insert a digit':
                var str = output.toString() + operation.number.toString()
                output = parseInt(str)
                break
              case 'Convert digits':
                var str = output.toString()
                var arr = str.split('')
                for(var x = 0; x < arr.length; x++){
                  if(arr[x] == operation.initial_number){
                    arr[x] = operation.output_number
                  }
                }
                str = ''
                for(var x = 0; x < arr.length; x++)
                {
                  str = str + arr[x]
                }
                output = parseInt(str)
                break
              case 'Sum the digits':
                var str = output.toString()
                var arr = str.split('')
                output = 0
                for(var x = 0; x < arr.length; x++){
                  output = output + parseInt(arr[x])
                }
                break
              case 'Mirror the digits':
                var str = output.toString()
                var arr = str.split('')
                var arr_length = arr.length

                for(var x = arr_length - 1; x >= 0; x++){
                  arr.push(arr[x])
                }

                output = 0
                for(var x = 0; x < arr.length; x++){
                  output = output + parseInt(arr[x])
                }
                break
              default:
                break
          }

          return output
        },

        generate_solution_string: function(operation){

          // create a string
          var string = ''

          // generate value
          switch(operation.type){
              case 'Add':
                  string = '+' + operation.number
                  break
              case 'Subtract':
                  string = '-' + operation.number
                  break
              case 'Multiply':
                  string = '*' + operation.number
                  break
              case 'Divide':
                  string = '/' + operation.number
                  break
              case 'Delete a digit':
                  string = '<<'
                  break
              case 'Flip the sign (+/-)':
                  string = '+/-'
                  break
              case 'Insert a digit':
                  string = operation.number
                  break
              case 'Convert digits':
                  string = operation.initial_number + '=>' + operation.output_number
                  break
              case 'Sum the digits':
                  string = 'SUM'
                  break
              case 'Mirror the digits':
                  string = 'Mirror'
                  break
              default:
                  string = ''
                  break
          }

          // return string
          return string

        }

        /*
          # Information #
          Operation Structure:

          type: 'Select a type',
          number: 0,
          initial_number: 0,
          output_number: 0,
          string: '',

          Possible Operation Types:
          - Select a type
          - Add
          - Subtract
          - Multiply
          - Divide
          - Delete a digit
          - Flip the sign (+/-)
          - Insert a digit
          - Convert digits
          - Sum the digits
          - Mirror
        */
    }

}
</script>

<style scoped>
    a{
        text-decoration: none;
    }
</style>
