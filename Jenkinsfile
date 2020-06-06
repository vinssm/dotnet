#!groovy


@Library('jenkins-global-lib') _

import com.company.project.*
def util = new com.company.project.util()

def AgentName='Windows_10_Agent'
def anyBuildFailed='false'

/*def notifySuccess() {
		emailext (
			subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: '${JELLY_SCRIPT, template="html"}',
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}

	def notifyFailure() {
		emailext (
			subject: "Failure: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: '${JELLY_SCRIPT, template="html"}',
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}

	def emailDownloadLink(String artifactUrl) {
		emailext (
			subject: "Build Release: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: "URL: $artifactUrl",
			mimeType: 'text/html',
			to: "vallab.v@gmail.com",
			from: "DevOps <devops.local.smtp@gmail.com>",
			replyTo: "vallab.v@gmail.com",
			//recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}  */


/* node {
       checkout scm
	data = readYaml file: 'input.yaml'
     } */


pipeline {
    agent none
	 options {
		 skipDefaultCheckout() // Don't checout automatically
		}

    stages {
        stage('Build Preparation') {
            agent { label "${AgentName}"  }
				steps {
						script {
							deleteDir()
							checkout scm
							echo "Checkout is complete"
							bat 'git clone "https://github.com/vinssm/CommonRepo.git"'
						}
                   }
              }

	stage('Build') {
        agent { label "${AgentName}"  }
			steps {
				script {
					Component_details = readYaml file: 'WebApp1\\input.yaml'
					env.AppName= "${Component_details.App.App_name}"
					env.CompName= "${Component_details.App.Comp_name}"
					env.project_file= "${Component_details.App.project_file}"
					//for (String item : build_file.split() ) {
					//	env.project_file=item
						echo "##### ${AppName}     ######################"
						echo "##### ${CompName}     ######################"
						echo "##### ${BUILD_NUMBER}  ######################"
						echo "##### ${WORKSPACE}     ######################"
						echo "##### ${project_file}  ######################"
					util.build(WORKSPACE,project_file)
					

				}
			}
		}


	stage('create_package') {
        agent { label "${AgentName}"  }
			steps {
				script {
					// Component_details = readYaml file: 'WebApp1\\input.yaml'
					env.AppName= "${Component_details.App.App_name}"
					env.CompName= "${Component_details.App.Comp_name}"
					// env.published_path= "${Component_details.App.published}" 
					env.project_file= "${Component_details.App.project_file}"
					env.published_path= "${Component_details.App.published}"
					//for (String item : build_file.split() ) {
					//	env.project_file=item
						echo "These parameters are required to Copy the Build Output to NAS"
						echo "##### ${AppName}     ######################"
						echo "##### ${CompName}     ######################"
						echo "##### ${BUILD_NUMBER}  ######################"
						echo "##### ${WORKSPACE}     ######################"
						echo "##### ${project_file}  ######################"
						echo "##### ${published_path}  ######################"
						// echo "##### ${CommitNumber}  ######################"
						env.published_path= "${WORKSPACE}\\${published_path}"
						echo "@@@@@@@@@@@@@@@@@ Build Output Location: ${published_path}"
						echo "========================================================================="
					util.create_package(WORKSPACE,project_file,published_path)
					

				}
			}
		}

	}
}


	  /*  stage('Run the Unit Tests') {
	    	steps {
	    		script {
			        print "Executing the unit tests ... "
		     		util.executeUnitTests() 
			    }
	        }
	    }   */

	   /* stage ('Upload to Artifactory') {
	    	steps {
	    		script {
			        print "artifactory"
		     		util.uploadToArtifactory() 
			    }
	        }
	    }   */


      /*  stage('Deploy to Servers') {
            steps {
	    		script {
		     		util.deploy() 
	        	}
            }
        } 
} 


/*	post {
        failure {
        	script {
        		notifyFailure()
        	}
        }
    }
}

  */
