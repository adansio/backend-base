pipeline {

	agent any
	environment {
		NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
	}
	stages {
		stage('etapa construccion app'){
			agent{
				docker {
					image 'node:alpine3.20'
					reuseNode true
				}
			}
			stages{
				stage ("install"){
					steps {
						sh 'npm install'
					}
				}
				stage ("test"){
					steps {
						sh 'npm run test'
					}
				}
				stage ("build"){
					steps {
						sh 'npm run build'
					}
				}
			}
		}
		stage('constru app'){
			steps{
				script{
					docker.withRegistry("https://us-central1-docker.pkg.dev","gcp-registry"){
					sh 'docker build -t backend-base .'
					sh 'docker tag backend-base us-central1-docker.pkg.dev/expertis-classroom/docker-repository/backend-base:amorales'
					sh 'docker push us-central1-docker.pkg.dev/expertis-classroom/docker-repository/backend-base:amorales'
					}
				}
			}
		}
	}
}
