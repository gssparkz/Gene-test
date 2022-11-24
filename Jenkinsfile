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

       stage('Run tests') {
          steps{
            sh 'mvn clean test'
            step([$class: 'JacocoPublisher', 
                execPattern: 'target/*.exec',
                classPattern: 'target/classes',
                sourcePattern: 'src/main/java',
                exclusionPattern: '**/util/**,**/domain/**,**/springboot/*.class,**/exception/**,**/configuration/**,src/test*'
            ])
          } 
        }
        
        stage('Build project') {
            steps {
                sh 'mvn -DskipTests clean package'
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
                    
                    waitForQualityGate abortPipeline: true, credentialsId: 'jenkins-sonar-token'
                }
            }
        }



    }

}