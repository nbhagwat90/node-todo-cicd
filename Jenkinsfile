pipeline {
	agent any 
	stages{
		stage("Code"){
			steps{git url: "https://github.com/nbhagwat90/node-todo-cicd.git", branch:"master"}
		             }
	
	    stage("build and test"){
			steps{
			    echo" build is created and tested"
			    sh 'docker build . -t nbhagwat90/node-todo-cicd:latest'
		         }
		                       }
		
		stage("push to repo"){
			steps{
			   echo 'logging in to dockehub and push image'
			withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPassword')])
			{
		            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"     
		            sh "docker push nbhagwat90/node-todo-cicd:latest"
			}
		         }
			                 }   
				             
	
		stage("deploy"){
			steps{
			    echo"app is deployed"
			    sh "docker-compose down && docker-compose up -d"
			}
			
		               }
		   }
          }
