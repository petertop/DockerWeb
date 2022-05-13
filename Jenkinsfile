pipeline{
    agent any
    stages{
        stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
        }
        stage('Docker Build') {
         steps {
            powershell(script: 'docker images -a')
            powershell(script: """
               docker build -t skb-webserver-image:v1 .
               docker images -a
            """)
         }  
        }
        stage('Docker Run Container') {
         steps {
            powershell(script: 'docker run --name web-dev -d -it -p 80:80 skb-webserver-image:v1')
         }
      }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}