pipeline {
  agent any
  stages {
    stage('compilar') {
      parallel {
        stage('compilar') {
          agent {
            node {
              label 'ubuntu'
            }

          }
          steps {
            sh 'mvn clean package'
            archiveArtifacts(artifacts: '**/*.war', fingerprint: true, onlyIfSuccessful: true)
          }
        }
        stage('checkstyle') {
          agent {
            node {
              label 'ubuntu'
            }

          }
          steps {
            checkstyle()
          }
        }
      }
    }
    stage('aprobar') {
      steps {
        input(message: 'aprobar despliegue', ok: 'SI')
      }
    }
    stage('despliegue') {
      agent {
        node {
          label 'windows'
        }

      }
      steps {
        copyArtifacts 'maven-project'
      }
    }
  }
}