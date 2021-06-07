pipeline {
	agent any
	environment {
	    MAVEN_HOME = tool('Maven')
	}
	stages {
		stage("Compile") {
			steps {
				sh "${MAVEN_HOME}/bin/mvn compile"
			}
		}
		stage("Unit test") {
			steps {
				sh "${MAVEN_HOME}/bin/mvn test"
			}
		}
	}
	
	post {
		always {
			step([$class: 'JacocoPublisher',
				execPattern: 'target/*.exec',
				classPattern: 'target/classes',
				sourcePattern: 'src/main/java',
				exclusionPattern: 'src/test*'
			])
		}
	}
}
