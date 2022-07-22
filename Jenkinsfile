pipeline{

    agent {label 'master'}
    parameters {
        choice(
            choices: ['nao' , 'sim'],
            description: '',
            name: 'ESTAGIO1')
        choice(
            choices: ['nao' , 'sim'],
            description: '',
            name: 'ESTAGIO2')
    }
    triggers{

        pollSCM '* * * * *'
        
       // GenericTrigger(    
       //      causeString: 'Triggered on $ref',
       //      token: 'abc123'
       // )
    }

    environment {
    
    // ================================================================================
         APPPOOLFINCONTROLELOJAS = "PLSS-Fin_controlelojas"
        

    }
    stages{

        stage('Verificando Alterações'){
            when{
                anyOf {changeset "alteracoes"; triggeredBy 'UserIdCause'}
                
            }
            
            stages {
                stage("Buildfalha")
                   {               
                   steps{
                        

                        catchError(message: 'O estagio falhou', stageResult: 'FAILURE') {
                            script{
                                                   
                                sh "natan"
                            }
                        }
                   }
                   
                }
                stage("sucesso")
                   {               
                   steps{
                       script{
                            sh "ls -lah"    
                       }
                   }
                }   
                
                
            }
            post {
                
                always {
                    
                    cleanWs()
                    
                }
            } 
        }
    }    
}                 
