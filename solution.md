 const plateSize =  96
const samples = [['Sam 1','Sam 2'], ['Sam 3', 'Sam 4', 'Sam 5']]
const reagents = [['Reag A', 'Reag B', 'Reag C'], ['Reag X', 'Reag Y', 'Reag Z']]
const replicate = [5,5]

class SoftLab {
  constructor(number) {
    if(number === 96){
      this.rows = 8
      this.columns = 12
      this.matrix = new Array(this.rows).fill().map(() => new Array(this.columns).fill(null));
    }
    if(number === 384){
      this.rows = 16
      this.columns = 24
      this.matrix = new Array(this.rows).fill().map(() => new Array(this.columns).fill(null))
    } 
  }
}

function experiment(plateSize, samples, reagents, replicate){
    const result = []
    const softlab = new SoftLab(plateSize)
    let matrix = softlab.matrix
    let row = 0
    let column = 0
    samples.forEach((experiment, index) => {
      for(let sample of experiment){
       for(let i = 0; i < replicate[index]; i++){
        for(let reagent of reagents[index]){
            if(matrix[row][column] === null && column !== softlab.columns){
              matrix[row][column] = [sample,reagent]
              column++
            }else if(row !== softlab.rows-1 && matrix[row][column] === undefined){
              row++
              column = 0
              matrix[row][column] = [sample,reagent]
              column++
            }
          else {
              result.push("result",matrix)
              matrix = new SoftLab(plateSize).matrix
              row = 0
              column = 0
              matrix[row][column] = [sample,reagent]
              column++
          }
        }
      }
     }
    })
    result.push(matrix)
    return result
}
console.log(experiment(plateSize, samples, reagents, replicate))