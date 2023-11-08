pipeline{
    agent any



    stages {


        stage('Getting project from Git') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/main']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/marwenesprit/devops.git']]])
            }
        }


       stage('Cleaning the project') {
            steps{
                	sh "mvn -B -DskipTests clean  "
            }
        }



        stage('Artifact Construction') {
            steps{
                	sh "mvn -B -DskipTests package "
            }
        }



         stage('JUnit') {
            steps{
                	sh "mvn -B -DskipTests clean  "
            }
        }


        stage('SONARQUBE') {
            steps{

             		sh " mvn clean verify sonar:sonar -Dsonar.projectKey=DevOps_Project -Dsonar.projectName='DevOps_Project' -Dsonar.host.url=http://192.168.56.2:9000 -Dsonar.token=sqp_313fd4947b5c9b8ca0ba0214ca027607fd9955f8 "
            }
        }


        stage('Publish to Nexus') {
            steps {


  sh 'mvn deploy'


            }
        }

stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t marwen/spring-app:Marwen .'
                          }
                      }
                  }

                  stage('login dockerhub') {
                                        steps {
				sh 'docker login -u marwen --password dckr_pat_0iaom9peVjYUg0VIvUkeT-5V4bg'
                                            }
		  }

	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push marwen/spring-app:Marwen'
                                            }
		  } 

 /* stage('clone frontend'){
         steps{
             script{
                   checkout([$class: 'GitSCM', branches: [[name: '*//* main']], extensions: [], userRemoteConfigs: [[url:"https://github.com/housseml17/front.git"


]]])
             }
         }

 } */

/*  stage("build and push frontend docker image") {
        
         
            steps {
                script {
                     
             sh 'docker login -u toumi15 --password dckr_pat_0iaom9peVjYUg0VIvUkeT-5V4bg'
         
             sh "docker push toumi15/front-app:Toumi"
           
                }
            }
                
                
             
                
            } */


     
	  /*   stage('Build Frontend Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t toumi15/front-app:Toumi .'
                          }
                      }
                  }

 stage("Push Frontend Docker image") {


            steps {
                script {

             sh 'docker login -u toumi15 --password dckr_pat_0iaom9peVjYUg0VIvUkeT-5V4bg'

             sh "docker push toumi15/front-app:Toumi"

                }
            }




            } */




	   

	   


}




}

