  pipeline{

   agent any

    stages{

     stage('Checkout'){

      steps{

       git branch: "main", url: 'https://github.com/gayatribandgar/kubernetes-demo.git'

     }

    }

     stage('Build'){

            steps{

              sh 'chmod a+x mvnw'

             sh './mvnw clean package -DskipTests=true'

             }

             post{

                 always{

                      archiveArtifacts 'target/*.jar'

                      }

                 }

              }

           stage('DockerBuild') {

               steps {

                     sh 'docker build -t gayatribandgar/g3-allergy-service-demo:allergy-service-image .'

                      }

                   }

                stage('Login') {

                     steps {

                         sh 'echo Gayatri1234@ | docker login -u gayatribandgar --password-stdin'

                           }

                      }

                    stage('Push') {

                            steps {

                         sh 'docker push gayatribandgar/g3-allergy-service-demo:allergy-service-image'

                                 }

                }
                        stage('kubernetes deployment'){
                          steps{sh 'kubectl apply -f allergy-service-deployment.yml'
                          }
        
         }

                }

        
        }

      