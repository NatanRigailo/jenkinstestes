pipeline{

    agent {label 'master'}

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
                changeset "alteracoes"
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
                   retryBuild {
                        rerunIfUnstable()
                        retryLimit(3)
                        progressiveDelay(60, 600)
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
