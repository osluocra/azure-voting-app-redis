pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            sh(script: 'echo "Hello World"')
            echo "$GIT_BRANCH"
            
         }
     }
   }
}
