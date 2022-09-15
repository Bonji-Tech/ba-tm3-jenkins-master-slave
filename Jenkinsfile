pipeline{
  agent {
    label {
      label 'slave1'
    }
  }
  stages{
    stage('version-control'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/Bonji-Tech/ba-tm3-jenkins-master-slave.git']]])
      }
    }
    stage('parallel-job'){
      parallel{
        stage('sub-job1'){
          steps{
            echo 'action1'
          }
        }
        stage('sub-job2'){
          steps{
            echo 'action2'
          }
        }
        stage('sub-job3'){
            steps{
                echo 'action3'
            }
        }
      }
    }
    /*
    stage('codebuild'){
      agent {
        label {
          label 'slave2'
        }
      }
      steps{
        sh 'cat /etc/passwd'
      }
    }
    */
    stage('Jenkins-status'){
        agent {
            label {
                label 'slave3'
            }
        }
			steps{
				sh 'lsblk'
        sh '/var/lib/jenkins/workspace/monitor.sh'
			}
		}
  }
}