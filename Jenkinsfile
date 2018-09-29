pipeline {
  agent any
  stages {
    stage('Install') {
      steps {
        bat 'C:\\Users\\Cleber\\Desktop\\Jenkins\\install.bat'
      }
    }
    stage('Compile') {
      parallel {
        stage('SendMail_1') {
          steps {
            emailext(subject: 'Aprobar Compilacion', body: 'Se requiere Aprobación para la compilación', attachLog: true, to: 'everglz')
          }
        }
        stage('Aprove_1') {
          steps {
            input(message: 'Aprobar Compilación', submitter: 'everglz')
          }
        }
      }
    }
    stage('Commit') {
      parallel {
        stage('SendMail_2') {
          steps {
            emailext(subject: 'Aprobar Commit', attachLog: true, to: 'laugza', body: 'Favor de Aprobar el Commit')
          }
        }
        stage('Aprove_1') {
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
    stage('Approved') {
      steps {
        emailext(subject: 'Aprobado', body: 'Se realizó el Commit a Master', attachLog: true, to: 'everglz', replyTo: 'laugza, ianglz')
      }
    }
  }
}