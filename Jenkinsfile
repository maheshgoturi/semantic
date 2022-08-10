pipeline {

	agent any

	stages {
		stage('SetGlobals'){
			steps {
				script {
					_gitScmVars = checkout scm
					gitBranch = _gitScmVars.GIT_BRANCH
					CMABaseVersion = '2.0'
					println "Git branch: ${gitBranch}"
					currentBuild.setDescription("${appVersion} <br> ${env.NODE_NAME}")
				}
			}
		}
		
		//Build stage start
		stage('Build'){
			steps {
				script {

						println "INFO: Building ${appVersion}"

				}
			}
		}
		//Build stage finished
		
		//Deploy stage start
        stage('Deploy') {
			steps {
				script {

					println "INFO: Deploying $appVersion"

				}
			}
        }
		//Deploy stage finished
		
		//Tag stage start
        stage('tag') {
			steps {
				script {
					if ('main'.equals(env.BRANCH_NAME)) {
						try {
							sh "chmod +x ./tag-release"
							println "Executing sh ./tag-release -b ${gitBranch} -m 'Tagging ${gitBranch} branch' -t 'major'"
							//sh "./tag-release -b ${gitBranch} -m 'Tagging ${gitBranch} branch' -t 'major'"
						} catch (Exception e) {
							println "Failed to tag the build. Marking the build as UNSTABLE. Exception: ${e}"
							currentBuild.result = 'UNSTABLE'
						}
					}
				}
			}
        }
		//Tag stage finished
	}
} 
