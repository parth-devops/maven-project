pipeline{
    agent any
    tools{
        jdk 'Java8'
        maven 'Maven'

    }
    stages{
        stage('initializing'){
            steps{
                echo "This is initializing stage"
            }
        }
        stage('Build'){
            steps{
                echo "This is Build stage"
                sh label: '', script: 'mvn clean package checkstyle:checkstyle'
            }
            post {
                success{
                echo "Archiving Artifacts"
                archiveArtifacts '**/*.war'
                echo "JUnit Test Report"
                junit '**/surefire-reports/*.xml'
                echo "CheckStyle Reports"
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'clean package checkstyle:checkstyle', unHealthy: ''
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "This is Deploy stage"
                build 'Dev-Deploy'
            }
            timeout(1) {
            input 'Would you like to build the test job?'
            }
            build 'test'
        }
    }
}