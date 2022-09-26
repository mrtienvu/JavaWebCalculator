pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent any
    
    stages{
        stage('Checkout SCM')
        {
            steps{
            echo 'Cloning...'
            git 'https://github.com/mrtienvu/JavaWebCalculator.git'
            
            }
        }
      stage('Compile')
        {
            steps{
                echo 'Compiling...'
                sh 'mvn compile'
            }
        }
      stage('CodeReview')
        {
            steps{
                echo 'Reviewing...'
                sh 'mvn pmd:pmd'
            }
        }
        
      stage('UnitTesting')
        {
            steps{
                echo 'Testing...'
                sh 'mvn test'
            }
            post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
            }
        }  
       stage('Metric Check')
        {
            steps{
                echo 'Metric checking...'
                sh 'mvn cobertura:cobertura -Dcoberture.report.format=xml'
            }
        }     
          stage('Package')
        {
            steps{
                echo 'Packaging...'
                sh 'mvn package'
            }
        }  
            
    }
}
