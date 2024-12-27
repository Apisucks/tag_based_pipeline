// pipeline {
//     agent any

//     stages {
//             stage('Checkout') {
//                 steps {

//                     sh "git rev-parse HEAD"
//                     script {
//                         def currentHash = sh(
//                             script: "git rev-parse HEAD",
//                             returnStdout: true
//                         )

//                         def latestTag = sh(
//                             script: "git tag --sort=-committerdate | head -1",
//                             returnStdout: true
//                         )

//                         def latestTagHash = sh(
//                             script: "git rev-parse -n 1 ${latestTag}",
//                             returnStdout: true
//                         )
                            
//                         if (currentHash.equalsIgnoreCase(latestTagHash)) {
//                             checkout([$class: 'GitSCM',
//                                 branches: [[name: "refs/tags/${latestTag}"]],
//                                 userRemoteConfigs: [[url: 'https://github.com/Apisucks/ci_pipeline_jenkins.git']]
//                             ])
//                         }

//                     }
//                     sh "git rev-parse HEAD"
//                 }
//         }
//         stage('Build') {
//             steps {
//                 echo 'Build in progress from Repo'    
//                 sh "cat README.md"
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 echo 'Deploy in progress from Repo'    
//             }
//         }
//     }
// }

pipeline {
    agent any

    environment {
        IS_TAG = false
    }

    stages {
        stage('Check Trigger') {
            steps {
                script {
                    // Check if the build was triggered by a tag
                    if (env.GIT_REF?.contains('refs/tags/')) {
                        IS_TAG = true
                        env.GIT_TAG = env.GIT_REF.split('refs/tags/')[1]
                    }
                }
            }
        }

        stage('Run for Tags') {
            when {
                expression {
                    return IS_TAG
                }
            }
            steps {
                echo "Triggered by a tag: ${env.GIT_TAG}"
                // Add your tag-specific build steps here
            }
        }
    }
}
