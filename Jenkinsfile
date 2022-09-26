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
            post {
                success {
                    cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                }
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
