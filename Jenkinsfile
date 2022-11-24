pipeline{
    
    agent any 
    
    tools {
        maven 'maven-3.8.6'
    }
     
    stages {
        
        stage('Git Checkout'){           
                          
                             
             steps{
                echo 'Brach to build : ' + params.build_tag
                checkout([$class: 'GitSCM',
                          branches: [[name: "${params.build_tag}"]],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          gitTool: 'Default',
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/gssparkz/Gene-test.git']],
                          
                ])
                }
            

            
        }

       stage('Unit Testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }



        stage('Integration Testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }




        stage('Maven Build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }


        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'jenkins-sonar-token') 
                    {
                       sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }



        stage('Quality gate status'){
            
            steps{
                
                script{
                    
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonar-token'
                }
            }
        }



    }

}