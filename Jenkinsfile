pipeline {
  agent {
    label ''
  }
  stages {
    stage('first stage') {
      steps {
        timeout(time: 5, unit: 'MINUTES') {
          echo 'We\'re not doing anything particularly special here.'
          echo 'Just making sure that we don\'t take longer than five minutes'
          echo 'Which, I guess, is kind of silly.'
          bat 'mvn -version'
        }
        
      }
      post {
        success {
          echo 'Only when we haven\'t failed running the first stage'
          
        }
        
        failure {
          echo 'Only when we fail running the first stage.'
          
        }
        
      }
    }
    stage('second stage') {
      tools {
        maven 'M3'
      }
      steps {
        echo 'This time, the Maven version should be 3.3.9'
        bat 'mvn -version'
      }
    }
    stage('third stage') {
      steps {
        parallel(
          "one": {
            echo 'I\'m on the first branch!'
            
          },
          "two": {
            echo 'I\'m on the second branch!'
            
          },
          "three": {
            echo 'I\'m on the third branch!'
            echo 'But you probably guessed that already.'
            
          }
        )
      }
    }
    stage('Fourth Stage') {
      steps {
        echo 'THE END'
      }
    }
  }
  tools {
    jdk 'J8'
    maven 'M3'
  }
  environment {
    FOO = 'BAR'
  }
  post {
    always {
      deleteDir()
      
    }
    
    success {
      mail(from: 'bob@example.com', to: 'adrien.stadler@gmail.com', subject: 'That build passed.', body: 'Nothing to see here')
      
    }
    
    failure {
      mail(from: 'bob@example.com', to: 'adrien.stadler@gmail.com', subject: 'That build failed!', body: 'Nothing to see here')
      
    }
    
  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 60, unit: 'MINUTES')
  }
}