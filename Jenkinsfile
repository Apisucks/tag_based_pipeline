pipeline {
    agent any

    stages {
            stage('Checkout') {
                steps {

                    sh "git rev-parse HEAD"
                    script {
                        def currentHash = sh(
                            script: "git rev-parse HEAD",
                            returnStdout: true
                        )

                        def latestTag = sh(
                            script: "git tag --sort=-committerdate | head -1",
                            returnStdout: true
                        )

                        def latestTagHash = sh(
                            script: "git rev-parse -n 1 ${latestTag}",
                            returnStdout: true
                        )
                            
                        if (currentHash.equalsIgnoreCase(latestTagHash)) {
                            checkout([$class: 'GitSCM',
                                branches: [[name: "refs/tags/${latestTag}"]],
                                userRemoteConfigs: [[url: 'https://github.com/Apisucks/ci_pipeline_jenkins.git']]
                            ])
                        }

                    }
                    sh "git rev-parse HEAD"
                }
        }
        stage('Build') {
            steps {
                echo 'Build in progress from Repo'    
                sh "cat README.md"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy in progress from Repo'    
            }
        }
    }
}