pipeline{
    agent any
    tools{
        type 'jdk'
        type 'maven'

    }
    stages{
        stage('initializing'){
            steps{
                echo "This is initializing stage"
                sh label: '', script: 'clean package checkstyle:checkstyle'
            }
        }
        stage('Build'){
            steps{
                echo "This is Build stage"
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
            }
        }
    }
}