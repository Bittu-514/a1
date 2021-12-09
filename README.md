node('main'){
  properties([
    parameters([
      choice(
        choices: ['ONE', 'TWO', 'THREE', 'FOUR', 'FIVE'], 
        name: 'CHOCIE_Param'
      ),
      booleanParam(
        defaultValue: true, 
        description: '', 
        name: 'BOOLEAN'
      ),
      text(
        defaultValue: '''
        default value for Multi Line
        ''', 
        name: 'MULTI_LINE_STRING'
      ),
      booleanParam(
        defaultValue: true, 
        description: '', 
        name: 'Update_Param'
      ),
      string(
        defaultValue: 'Siva AWS #$@!%', 
        name: 'STRING_PARAMETER', 
        trim: true
      )
   ])
 ])
  if(params.Update_Param){
    println('This Update_Param flag was set to True. SO its only going to update parameters and skip code execution part')
    currentBuild.result = 'SUCCESS'
    return
  }
stage('Stage 1'){    
    if(params.BOOLEAN == true){
      println("As value is " + BOOLEAN)
      timeout(unit: 'SECONDS', time: 60) {
          def returnValue = input message: 'Need some input', submitter: '123456',
          parameters: [
            string(defaultValue: '', description: '', name: 'Name'),
            choice(choices: ['Siva' , 'Vignesh'], name: 'CHOCIE_Param')
          ]
          println(returnValue)
      }
      
    }
  }
  stage('Stage 2'){
    println('Hello CHOCIE-Param!! ' + CHOCIE_Param)
    println("Hello BOOLEAN!! $BOOLEAN")
    println("Hello MULTI-LINE-STRING!! ${MULTI_LINE_STRING}")
    println('Hello STRING-PARAMETER!! ' + STRING_PARAMETER)
  }
}
