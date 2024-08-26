pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo("build the war")
            }
        }

        stage("Deploy to QA"){
            steps{
                echo("deploy to qa")
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/AshwathaDS/PostmanCollections'
            }
        }
        stage('Run API Postman Collection Test Cases') {
            steps {
                bat 'newman run ./SampleCollection.json  -e ./SampleEnv.json -n 1 -r htmlextra,cli --reporter-htmlextra-export ./results/SampleReport.html'
            }
        }
        stage('Publish HTML Extra Report'){
            steps{
                     publishHTML([allowMissing: false,
                                  alwaysLinkToLastBuild: false, 
                                  keepAll: true, 
                                  reportDir: 'results', 
                                  reportFiles: 'SampleReport.html', 
                                  reportName: 'HTML Extra API Report', 
                                  reportTitles: ''])
            }
        }

        stage("Deploy to PROD"){
            steps{
                echo("deploy to PROD")
            }
        }
    }
}

