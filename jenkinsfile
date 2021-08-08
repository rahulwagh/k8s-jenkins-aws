node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/MEsSayed/k8s-jenkins-aws2'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t messayed-devops-capstone .'
        sh 'docker image list'
        sh 'docker tag messayed-devops-capstone messayed/messayed-devops-capstone:messayed-devops-capstone'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u messayed -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  messayed/messayed-devops-capstone:messayed-devops-capstone'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
