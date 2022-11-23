pipeline{
    
    agent any 

    tools {
        maven 'Maven 3.8.6'
        jdk 'Java 11.0.17.8.1'
    }
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'dev', url: 'https://github.com/gssparkz/Gene-test.git'
                }
            }
        }

       stage('Unit Testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }


    }

}