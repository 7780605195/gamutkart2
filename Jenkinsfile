pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}

//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "roopa" scp target/gamutkart.war roopa@172.17.0.3:/rani/apache-tomcat-8.5.43/webapps'
				sh 'sshpass -p "roopa" ssh roopa@172.17.0.3 "JAVA_HOME=/software/jdk1.8.0_211" "/rani/apache-tomcat-8.5.43/bin/startup.sh"'
	    	}
		}
    }
}
