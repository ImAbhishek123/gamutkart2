pipeline {
    agent any

	tools {
		jdk 'jdk11'
	}

//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                         sshpass -p "abhi" scp target/gamutkart-1.1-SNAPSHOT.war  abhi@172.17.0.2:/home/test/apache-tomcat-10.1.48/webapps
                          sshpass -p "abhi" ssh abhi@172.17.0.2 /home/test/apache-tomcat-10.1.48/bin/startup.sh 
            }
        }
    }
}
