pipeline {
    agent any

//	tools {
//		maven 'maven3.6'
//	}
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
                sh 'sshpass -p "Hari2739@" scp target/gamutgurus.war Hari-1@172.17.0.2:/home/Hari-1/apache-tomcat-9.0.62/webapps'
                sh 'sshpass -p "Hari2739@" ssh Hari-1@172.17.0.2 "/home/Hari-1/apache-tomcat-9.0.62/bin/startup.sh"'
            }
        }
    }
}
