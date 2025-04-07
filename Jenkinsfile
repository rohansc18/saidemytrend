pipeline{
    agent any
    environment{
         PATH = "/opt/maven/bin:$PATH" 
          } 
    stages{
        stage("build"){
            steps{
                echo "...build started..."
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "...build completed..."
                 } 
        }
          stage("test"){
            steps{
                echo "...unit test started..."
                sh 'mvn surefire-report:report'
                echo "...unit test completed..."
                 } 
        }

        stage("Quality Gate"){
            steps{ 
              script{ 
                 timeout(time:1 , unit:'Hours'){
                   def qg = waitForQualityGate()
                       if(qg.status != 'ok'){
                           error "Pipeline aborted due to quality gate failure : ${qg.status}"  
                                            } 
                                               }
                    }
                 }
        }
    }
}

