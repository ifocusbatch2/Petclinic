pipeline{

    agent any
    
    tools {
	    maven "Maven"
        
	 	}


    stages{

       stage('clone the project'){
        steps{
            
           git branch: 'main', url: 'https://github.com/jaiswaladi246/Petclinic.git'
          
        }

       }

       stage('Build the project'){
        steps{
           sh 'mvn clean install'
        }

       }

       stage('Test'){
        steps{
           sh 'mvn test'
        }

       }
       stage('published the test results'){
        steps{
           junit 'target/surefire-reports/*.xml'
        }

       }
       stage('publishedd the artifacts'){
        steps{
           archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
        }

       }

     stage('Sonarqube Analysis'){
        steps{
            mvn "clean verify sonar:sonar \
            -Dsonar.projectKey='spring-petclinic' \
            -Dsonar.projectName='spring-petclinic' \
            -Dsonar.host.url='http://localhost:9000' \
            -Dsonar.token=sqp_92e22c2e58430246c8b2f8dbd89a8b053c19197b"
        }

       }
    

       stage('Deploy to Tomcat Server'){
        steps{
           deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8080/')], contextPath: 'Ifocus Solutions Pvt Limited', war: 'target/*.war'
        }

       }


    }
}