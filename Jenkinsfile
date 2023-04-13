pipeline {
   agent any
   environment {
    PATH = "/usr/local/bin:${env.PATH}"
   }
   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            echo "PATH is: ${env.PATH}"
            sh(script: '/usr/local/bin/docker images -a')
            sh(script: """
               cd azure-vote/
               /usr/local/bin/docker images -a
               /usr/local/bin/docker build -t jenkins-pipeline .
               /usr/local/bin/docker images -a
               cd ..
            """)
         }
      }
      stage('Start test app') {
         steps {
            sh(script: """
               /usr/local/bin/docker-compose up -d
               ./scripts/test_container.sh
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            sh(script: """
               /usr/local/bin/docker-compose down
            """)
         }
      }
   }
}
