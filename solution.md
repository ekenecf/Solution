 const plateSize =  96
  const samples = [['Sam 1'], ['Sam 4', 'Sam 5', 'Sam 6']]
  const reagents = [['Reag X', 'Reag v', 'Reag W'], ['Reag Y', 'Reag Z']]
  const replicate = [2,2]

class SoftLab {
  constructor(number) {
    if(number === 96)
      this.matrix = new Array(8).fill(null).map(() => new Array(12).fill(null));
    if(number === 384)
      this.matrix = new Array(16).fill(null).map(() => new Array(24).fill(null))
  }
}

function experiment(plateSize, samples, reagents, replicate){
    const result = []
    const well = []
    samples.forEach((experiment, index) => {
      for(let sample of experiment){
       for(let i = 0; i < replicate[index]; i++){
        for(let reagent of reagents[index]){
           well.push([sample,reagent])
        }
      }
     }
    })
  
    let counter = 0
    console.log(well.length)
    const matrix = new SoftLab(plateSize).matrix
    for(let eachArray of matrix){
      if(counter === well.length - 1) break
      for(let position in eachArray){
        if(eachArray[position] === null){
          eachArray[position] = well[counter]
          counter++ 
        }
      }
    }
     return matrix
}

console.log(experiment(plateSize, samples, reagents, replicate))