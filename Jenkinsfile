pipeline {
  agent any
  stages {
    stage('Install') {
      steps {
        bat 'C:\\Users\\Cleber\\Desktop\\Jenkins\\install.bat'
      }
    }
    stage('SendMail_Compile') {
      parallel {
        stage('SendMail_1') {
          steps {
            emailext(subject: 'Aprobar Compilacion', body: 'Se requiere Aprobaci�n para la compilaci�n', attachLog: true, to: 'everglz')
          }
        }
        stage('Aprove') {
          steps {
            input(message: 'Aprobar Compilaci�n', submitter: 'everglz')
          }
        }
      }
    }
    stage('SendMail_Commit') {
      parallel {
        stage('SendMail_2') {
          steps {
            emailext(subject: 'Aprobar Commit', attachLog: true, to: 'laugza', body: 'Favor de Aprobar el Commit')
          }
        }
        stage('Aprove') {
          steps {
            input(message: 'Aprobar Commit', submitter: 'laugza')
          }
        }
        stage('Commit') {
          steps {
            bat 'C:\\Users\\Cleber\\Desktop\\Jenkins\\commit.bat'
          }
        }
      }
    }
    stage('SendMail_Aproved') {
      steps {
        emailext(subject: 'Aprobado', body: 'Se realiz� el Commit a Master', attachLog: true, to: 'everglz', replyTo: 'laugza, ianglz')
      }
    }
  }
}