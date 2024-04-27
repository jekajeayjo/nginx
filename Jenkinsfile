pipeline {

    environment {
        registry = "f-ksolutions"
        acPort = 1337
        dockerImage = ''
        }

    agent {
    node {
     label 'k-solutions-com'
     }
    }

    stages {
            stage('Delete old container') {
                        steps {
                            script {
                             try {
                           sh("java --version")
                           sh("docker stop f-ksolutions-nginx")
                           sh("docker rm f-ksolutions-nginx")
                           sh("docker rmi f-ksolutions-nginx")
                                        } catch (err) {
                                            echo err.getMessage()
                                        }
                            }
                         }
                    }
            stage('Build docker image') {
                 steps {
                     script {
                        echo "current build number: ${currentBuild.number}"
                        sh("docker build -t  f-ksolutions-nginx .")
                     }
                  }
             }
            stage('Run docker container') {
                 steps {
                     script {
                          sh(" docker run -td --restart unless-stopped -v /opt/certs/:/opt/certs  --name f-ksolutions-nginx -p 80:80 -p 443:443 f-ksolutions-nginx ")
                     }
                  }
             }
        }
}

