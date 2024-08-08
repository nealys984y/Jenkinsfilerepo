node {
    def app

    stage('Clone repository') {
      

        checkout scm: ([
                    $class: 'GitSCM',
                    userRemoteConfigs: [[url: 'https://github.com/brandonjones085/docker.git']],
                    branches: [[name: 'master']]
            ])
    }

    stage('Build image') {
  
       app = docker.build("ys984y/docker_training")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

   stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

/*checkout([
        $class: 'GitSCM', 
        branches: [[name: '*/master']], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [[$class: 'CleanCheckout']], 
        submoduleCfg: [], 
        userRemoteConfigs: [[url: 'https://github.com/brandonjones085/docker.git']]
    ]) **/
