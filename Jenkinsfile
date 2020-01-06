pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        dir(path: 'pact-provider') {
          sh 'mvn clean install'
        }

      }
    }

    stage('Sonar Scan') {
      steps {
        sh 'echo "Sonar Scan"'
      }
    }

    stage('Running Provider') {
      steps {
        dir(path: 'pact-provider') {
          sh 'mvn spring-boot:run &'
        }

      }
    }

    stage('Start PactBroker') {
      steps {
        dir(path: 'pact-broker') {
          sh 'sudo /usr/local/bin/docker-compose up -d'
        }

      }
    }

    stage('Verify Pact') {
      steps {
        dir(path: 'pact-provider') {
          sh 'mvn pact:verify'
        }

      }
    }

    stage('Close PactBroker') {
      steps {
        dir(path: 'pact-broker') {
          sh 'sudo /usr/local/bin/docker-compose down'
        }

      }
    }

    stage('Build Provider') {
      steps {
        dir(path: 'pact-provider') {
          sh '/usr/local/bin/docker build -t pact-provider .'
        }

      }
    }

    stage('Publish Provider To Repository') {
      steps {
        dir(path: 'pact-provider') {
          sh 'security unlock-keychain -p "5+5!=Ten" ~/Library/Keychains/login.keychain'
          sh '/usr/local/bin/docker login -u feihuo55 -p 20010413guo'
          sh '/usr/local/bin/docker tag $(/usr/local/bin/docker images --filter=reference=pact-provider --format "{{.ID}}") feihuo55/cdcdemo'
          sh '/usr/local/bin/docker push feihuo55/cdcdemo'
        }

      }
    }

  }
}