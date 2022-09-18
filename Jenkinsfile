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
    stage('git-clone'){
      parallel{
        stage('parallel-1'){
          steps{
            sh 'lscpu'
          }
        }
        stage('parallel-1a'){
          steps{
            sh 'free -m'
          }
        }
      }
    }  
    stage('systemcheck'){
      parallel{
        stage('free-memory'){
          steps{
            sh 'free -g'
          }
        }
        stage ('system-stat1'){
          steps{
            sh 'lscpu'
          }
        }
      }
    }
    stage('uptime'){
      parallel{
        stage('runtime'){
          agent {
            label{
              label 'slave2'
            }
          }
          steps{
            sh 'uptime'
          }
        }
        stage('system-stat2'){
          steps{
            sh 'lsblk'
          }
        }
      }
    }
    stage('codebuild'){
      parallel{
        stage('runtime'){
          agent {
            label{
              label 'slave3'
            }
          }
          steps{
            sh '/home/jenkins/workspace/monitor.sh'
          }
        }
        stage('system-stat2'){
          steps{
            sh 'cat /etc/passwd'
            sh 'whoami'
          }
        }
      }
    }
  }
}
