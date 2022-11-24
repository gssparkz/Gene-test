pipeline{
    
    agent any 
    
    tools {
        maven 'maven-3.8.6'
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