pipeline {
    agent any

//	tools {
//		jdk 'jdk8'
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
                sh 'sshpass -p "sameer" scp target/gamutgurus.war sameer@172.17.0.2:/home/sameer/proj/apache-tomcat-9.0.80/webapps'
                sh 'sshpass -p "sameer" ssh sameer@172.17.0.2 "/home/sameer/proj/apache-tomcat-9.0.80/bin/startup.sh"'
            }
        }
    }
}
