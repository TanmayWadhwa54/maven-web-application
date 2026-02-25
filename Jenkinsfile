pipeline {
        agent any
        stages {
	        stage("SCM") {
                     steps {
                            git 'https://github.com/TanmayWadhwa54/maven-web-application.git'
                            }
                          }

                stage("build") {
                     steps {
                             sh 'sudo mvn clean package'
                             }
                           }
                stage("build-image") {
                     steps {
                             sh 'sudo docker build -t java-repo:$BUILD_TAG .'
                             sh 'sudo docker tag java-repo1:$BUILD_TAG tanmaywadhwa54/pipeline-java1:$BUILD_TAG'
                             }
                }
                stage("dockerlogin") {
                     steps { 
		             withCredentials([string(credentialsId: 'pass', variable: 'pass_var')]) {
			     sh 'sudo docker login -u tanmaywadhwa54 -p ${pass_var}'
			     sh 'sudo docker push tanmaywadhwa54/pipeline-java1:$BUILD_TAG'
			     }
		     }
		      
		}
		stage("QAT TESTING") {
		     steps {  
		              sh 'sudo docker run -dit --name web10tom -p 8090:8080 tanmaywadhwa54/pipeline-java1:$BUILD_TAG'
                    } 
	       }


	        stage("test-website") {
	             steps { 
		             sh 'sudo sleep 20'
		             sh 'sudo curl --ipv4 http://localhost:8090'

                       }
	       }
}
}



















