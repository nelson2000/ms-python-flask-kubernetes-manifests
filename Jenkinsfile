node {

        def app
        // def repoUrlWithAuth = "https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ms-python-flask-kubernetes-manifests.git"
        // def sourceBranch = "main"

        stage("clone repository") {
            
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/nelson2000/ms-python-flask-kubernetes-manifests.git']])
        }


        stage("Update Git"){

            script {

                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github_cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME' )]){

                        sh "git config user.email nwajienelson@gmail.com"
                        sh "git config user.name nelson"
                        sh "echo 'below is echo workspace'"
                        sh "echo $WORKSPACE"
                        sh "echo 'below is ls workspace'"
                        sh "ls $WORKSPACE"
                        sh "echo 'below is ls -ltar'"
                        sh "ls -ltar"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+nwajienelson/pythonapp***+nwajienelson/pythonapp+g' deployment.yaml"
                        sh "sed -i 's+nwajienelson/pythonapp+nwajienelson/pythonapp:${DOCKERTAG}+g' deployment.yaml"
                        
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ms-python-flask-kubernetes-manifests.git HEAD:master"
                }  
                     
               
            }
        }

  

    }
}  


// def repoUrlWithAuth = "https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/ms-python-flask-kubernetes-manifests.git"
// def sourceBranch = "main"

// git push --repo=${repoUrlWithAuth} --set-upstream ${repoUrlWithAuth} ${sourceBranch}

// pipeline {
//     agent any
    
//     stages {
//         stage('Git Push') {
//             steps {
//                 script {
//                     // Configure Git user
//                     gitConfigureUser('John Doe', 'john.doe@example.com')
                    
//                     // Git push
//                     withCredentials([usernamePassword(credentialsId: '<credentials-id>', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
//                         sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@<repository-url> <branch-name>"
//                     }
//                 }
//             }
//         }
//     }
// }

// def gitConfigureUser(name, email) {
//     // Configure Git user name and email
//     sh "git config --global user.name '${name}'"
//     sh "git config --global user.email '${email}'"
// }

    // jenkins url 20.220.74.174:8085
