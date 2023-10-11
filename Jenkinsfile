pipeline {
    agent any

    environment {

    }

    stages {
        stage("Checkout Git") {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/stwins60/jenkins-demo.git']])
            }
        }

        stage("Reading Json and passing as environment variable") {
            steps {
                script {
                    def json = readJSON file: 'data.json'
                    sh "echo ${json}"
                    env.ENVIRONMENT = json.extra_vars.env
                    env.REGION = json.extra_vars.region
                    env.TEST_TYPE = json.extra_vars.test_type
                    env.ANALYTICS = json.extra_vars.analytics
                }
            }
        }

        stage("Use Environment variable") {
            steps {
                sh 'echo "Environment: $ENVIRONMENT"'
                sh 'echo "Region: $REGION"'
                sh 'echo "Test Type: $TEST_TYPE"'
                sh 'echo "Analytic: $ANALYTIC"'
            }
        }
    }
}