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
            
            stages {
                stage("Buildfalha")
                   {               
                   steps{


                        catchError(message: 'O estagio falhou', stageResult: 'NOT_BUILT') {
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
