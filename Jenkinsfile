pipeline {
  agent {
    kubernetes {
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {

    stage('build') {
      steps {
        container('maven') {
          dir('project') {
            echo 'check out the project'
            checkout([
              $class: 'GitSCM', 
              branches: [[name: '*/main']], 
              extensions: [], 
              userRemoteConfigs: [[url: 'https://github.com/rsmaxwell/example-java']]
            ])

            echo 'prepare the application'
            sh('./scripts/prepare.sh')

            echo 'build the application'
            sh('./scripts/build.sh')

            echo 'packaging the application'
            sh('./scripts/package.sh')

            echo 'testing the application'
            sh('./scripts/test.sh')

            echo 'deploying the application'
            sh('./scripts/deploy.sh')
          }
        }
      }
    }
  }
}
