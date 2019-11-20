pipeline {
    agent any
environment {
    VERSION = readMavenPom().getVersion()
}
    stages {
       stage ("version"){
	echo "$(version)"
	}
	 stage('Testing') {
            steps {
                    sh 'mvn test -Dtest=ControllerAndServiceSuite'
			sh 'mvn test -Dtest=IntegrationSuite'
                }
            }
        stage('Build') {
            steps {
		sh 'mvn package -DskipTests'
                 sh 'docker build -t="sarah1818/simple-project:latest" .'
 }
            }
        stage('Deploy') {
            steps {
		sh 'docker push sarah1818/simple-project:latest'
            }
        }
    
  stage('Testing Environment') {
            steps {
                echo "hello"
            }
        }
      stage('Staging') {
	when{
		expression{
		env.BRANCH_NAME=='developer'
		}
	}
            steps {
                echo "hello"
            }
        }
      stage('Production') {
	when{
		expression{
		env.BRANCH_NAME=='master'
		}
	}
            steps {
                echo "production"
            }
        }
    }
}

