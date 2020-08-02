pipeline
{
    agent any
    
        stages{
            stage('pre cleanup'){
                script{
                     sh label: '', script: 'docker system prune -f > /dev/null 2>&1'
                      cleanWs()
                }
            
                            }
            stage('Checkout from SCM'){
            
                 script{
                      git([url: 'https://github.com/Vijayarajamayuri/NodeApp', branch: 'master', credentialsId: 'Gthubid'])
                              }  
                                       }
            stage('Install NPM'){
                        script{
                             sh label: '', script: 'npm install'
                              }  
                                }
            stage('Build Docker'){
                 script{
                 sh label: '', script: 'docker build -t demoecr .'
                       }  
                                   }
            stage('Push docker image to ECR'){
                            script{
                  docker.withRegistry('https://662069790082.dkr.ecr.us-east-1.amazonaws.com/demoecr', 'ecr:us-east-1:AWSCredentials') {
                        docker.image('demoecr').push('latest')
                              }
                                   }  
                                     }
            stage('Post cleanup'){
                     script{
                         sh label: '', script: 'docker system prune -f > /dev/null 2>&1'  
                          cleanWs
                            }
                                }  
                
            }
        }
      

    
