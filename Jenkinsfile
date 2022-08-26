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
                        
            stages {
                stage("Buildfalha")
                   {
                    when{
                        anyOf {environment name: 'ESTAGIO1', value: 'sim';changeset "estagio1"}
                
                    }
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
                   when{
                        anyOf {environment name: 'ESTAGIO2', value: 'sim';changeset "estagio2"}
                
                   }
                   steps{
                       load "/envs/outroenv.groovy"
                       script{
                            sh "ls -lah"
                            sh "echo $OUTROENV"
                            sh "hostname"
                            
                       }
                   }
                }   
                
                
            }
            post {
                
                always {
                    discordSend description: "Pipeline do Job teste finalizou", footer: "", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: "https://discord.com/api/webhooks/961017653982543882/ynHLG0lBxEcMuaWOfegV10XG_N89mpwcm4Lx-6y3jIcY_3fQnjMn_U4NMT5crgjE_2fu"

                    cleanWs()
                    
                }
            } 
        }
    }    
}                 
