pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
   //   stage('Docker Build') {
   //       steps {
   //          //sh 'docker images -a'
   //          sh 'docker build -t jenkins-pipeline .'
   //          //sh 'docker images -a'
   //       }
   //    }
      // stage('Start test app') {
      //    steps {
      //       sh 'docker-compose up -d'
      //       sh './scripts/test_container.sh'
      //    }
      //    post {
      //       success {
      //          echo "App started successfully :)"
      //       }
      //       failure {
      //          echo "App failed to start :("
      //       }
      //    }
      // }
      // stage('Run Tests') {
      //    steps {
      //       sh 'python3 tests/test_sample.py'
      //    }
      // }
      // stage('Stop test app') {
      //    steps {
      //       sh 'docker-compose down'
      //    }
      // }
      stage('Push Container') {
         steps {
            echo "Workspace is $WORKSPACE"
            dir("$WORKSPACE/azure-vote") {
               script {
                  docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                     def image = docker.build('kingoamino/course:latest')
                     image.push()
                  }
               }
            }
         }
      }
      // docker tag local-image:tagname new-repo:tagname
      // docker push new-repo:tagname
   //    stage('Container Scanning') {
   //       parallel {
   //          stage('Run Anchore') {
   //             steps {
   //                pwsh(script: """
   //                   Write-Output "blackdentech/jenkins-course" > anchore_images
   //                """)
   //                anchore bailOnFail: false, bailOnPluginFail: false, name: 'anchore_images'
   //             }
   //          }
   //          stage('Run Trivy') {
   //             steps {
   //                sleep(time: 30, unit: 'SECONDS')
   //                // pwsh(script: """
   //                // C:\\Windows\\System32\\wsl.exe -- sudo trivy blackdentech/jenkins-course
   //                // """)
   //             }
   //          }
   //       }
   //    }
   //    stage('Deploy to QA') {
   //       environment {
   //          ENVIRONMENT = 'qa'
   //       }
   //       steps {
   //          echo "Deploying to ${ENVIRONMENT}"
   //          acsDeploy(
   //             azureCredentialsId: "jenkins_demo",
   //             configFilePaths: "**/*.yaml",
   //             containerService: "${ENVIRONMENT}-demo-cluster | AKS",
   //             resourceGroupName: "${ENVIRONMENT}-demo",
   //             sshCredentialsId: ""
   //          )
   //       }
   //    }
   //    stage('Approve PROD Deploy') {
   //       when {
   //          branch 'master'
   //       }
   //       options {
   //          timeout(time: 1, unit: 'HOURS') 
   //       }
   //       steps {
   //          input message: "Deploy?"
   //       }
   //       post {
   //          success {
   //             echo "Production Deploy Approved"
   //          }
   //          aborted {
   //             echo "Production Deploy Denied"
   //          }
   //       }
   //    }
   //    stage('Deploy to PROD') {
   //       when {
   //          branch 'master'
   //       }
   //       environment {
   //          ENVIRONMENT = 'prod'
   //       }
   //       steps {
   //          echo "Deploying to ${ENVIRONMENT}"
   //          acsDeploy(
   //             azureCredentialsId: "jenkins_demo",
   //             configFilePaths: "**/*.yaml",
   //             containerService: "${ENVIRONMENT}-demo-cluster | AKS",
   //             resourceGroupName: "${ENVIRONMENT}-demo",
   //             sshCredentialsId: ""
   //          )
   //       }
   //    }
   }
}
