pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            sh(script: 'echo "Hello World"')
            echo "$GIT_BRANCH"
            
         }
      }

      stage('Docker Build'){
         steps{
               sh(script:'docker images -a')
               sh(script:"""
                  
                  cd azure-vote/
                  pwd
                  ls -otr
                  cd ..
               
               """)
            }
      }

   }

}
