pipeline {
    agent any

    stages {
   stage('Dev build completed') {
            steps {
                // Checkout source code from the connected Git repo
               echo "dev completed build"
            }
        }

        stage('Clean workspace') {
            steps {
                // Checkout source code from the connected Git repo
               deleteDir()
            }
        }
        stage('Checkout Code') {
            steps {
                // Checkout source code from the connected Git repo
                git url: 'https://github.com/Hemanth2189856/JenkinsApi', branch: 'master'
            }
        }

        stage('Run Newman Tests') {
            steps {
                sh """
                    newman run ./BookingAPIs_Collection_ForJenkins.postman_collection.json \
                        -e ./BookingAPIEnv.postman_environment.json -n 3 \
                        -r cli,htmlextra,html
                """
            }
        }
stage('deploying to prod') {
            steps {
                // Checkout source code from the connected Git repo
               echo "deploying to prod"
            }
        }
    }

    post {
        always {
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'newman',
                reportFiles: '*.html',
                reportName: 'Newman HTML Report'
            ])
        }
    }
}