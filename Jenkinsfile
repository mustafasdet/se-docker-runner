// The following causes endless jenkins job because selenium grid is not exiting
// pipeline{
//     agent any
//     stages{
//         stage("Run Test") {
//             steps{
//                 sh "docker-compose up"
//             }
//         }
//         stage("Bring Grid Down") {
//             steps{
//                 sh "docker-compose down"
//             }
//         }
//     }
// }
pipeline{
    agent any
    stages{
        stage("Pull latest image") {
                steps{
                    sh "docker pull mustafasdet/se-docker"
                }
        }
        stage("Start grid") {
            steps{
                sh "docker-compose up -d hub chrome firefox"
            }
        }
        stage("Run tests") {
            steps{
                sh "docker-compose up search-module book-flight-module"
            }
        }
    }
	post{
		always{
// always >> will see the results in the specified directory
// we moved docker-compose down to here alse
		//Since a stage can be skipped. But post { always .. executed}
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
			sh "sudo rm -rf output/"
			// The above cmd is to reach output files easily.
		}
    }
}


// The following is the end code pulled from git
// pipeline{
// 	agent any
// 	stages{
// 		stage("Pull Latest Image"){
// 			steps{
// 				sh "docker pull vinsdocker/selenium-docker"
// 			}
// 		}
// 		stage("Start Grid"){
// 			steps{
// 				sh "docker-compose up -d hub chrome firefox"
// 			}
// 		}
// 		stage("Run Test"){
// 			steps{
// 				sh "docker-compose up search-module book-flight-module"
// 			}
// 		}
// 	}
// 	post{
// 		always{
// 			archiveArtifacts artifacts: 'output/**'
// 			sh "docker-compose down"
// 			sh "sudo rm -rf output/"
// 		}
// 	}
// }