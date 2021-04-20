pipeline {
    agent any

    stages {
        stage ("git clone") {
            steps {
                git credentialsId: 'Github', url: 'https://github.com/tejesh555/SKRLogin.git'
            }
        }

        stage ("build") {
            steps {
                sh "mvn clean install"
            }
        }

        stage ("publish") {
            steps {
                rtUpload (
                    serverId: 'myjfrog',
                    spec: '''{
                        "files": [
                            {
                            "pattern": "target/*.war",
                            "target": "skr"
                            }
                        ]
                    }''',
                
                    // Optional - Associate the uploaded files with the following custom build name and build number,
                    // as build artifacts.
                    // If not set, the files will be associated with the default build name and build number (i.e the
                    // the Jenkins job name and number).
                    buildName: "${ JOB_NAME }",
                    buildNumber: "${BUILD_NUMBER }"
                )
            }
        }


    }
}
