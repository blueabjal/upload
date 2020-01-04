node {
    stage('scm'){
       git 'https://github.com/blueabjal/new.git'
    }
    stage('build') {
        sh 'mvn clean install'
    }
    stage('build docker image') {
       sh 'docker build -t abjal/app:2.0 .'
    }
    stage('push to docker hub') {
          sh "docker login -u abjal -p abjal12345"
      sh 'docker push abjal/app:2.0'
    }
    stage('run container'){
        withCredentials([sshUserPrivateKey(credentialsId: '1dd31cd0-240d-4f40-a7a8-9d5839603935', keyFileVariable: 'pass', passphraseVariable: '', usernameVariable: 'username')]) {
            sh "ssh -i ${pass} ec2-user@10.0.1.228 'docker run -it -d -p 8080:8080 --name app abjal/app:2.0'"
           }
    }
}
