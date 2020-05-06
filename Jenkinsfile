pipeline {
    agent any
    triggers {
        cron('H */1 * * * ')
     }
    tools {
        maven 'M2_HOME'
      
    }
    stages {
      stage('Build'){
        steps {
          echo "Build step"
          sh 'mvn clean'
          sh 'mvn install'
          sh 'mvn package'
        }
      
      
      }
        stage('test '){
        steps {
            retry(1){
          echo  "test step"
            }
          sh 'mvn test'
        }
      
      
      }
        stage('deploy'){
        steps {
           sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker rmi -f jenkinsfile; docker build -t calvin2019/jenkinsfile .; docker tag jenkinsfile calvin2019/jenkinsfile; docker push calvin2019/jenkinsfile; docker run -d --name jenkinsfile-container -p 80:80 calvin2019/jenkinsfile', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//dockeruser', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
           
           
        }
      
      
      }
    
    }
    post {
        always {
            echo "Always display this message "
        }
        failure {
            echo "Job failed "
        }
        success {
            echo "Successful run "
        }
        unstable {
            echo "The job is unstable "
        }
    } 

}
