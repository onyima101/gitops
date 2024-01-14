node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("onyima101/jenkins-slave")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering ndcc-project-3-CDjob"
                build job: 'ndcc-project-3-CD', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
