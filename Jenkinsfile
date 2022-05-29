def imageName = 'olivier/movies-store'

node('workers'){
    stage('Checkout'){
        checkout scm
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality Tests'){
        sh "docker run --rm ${imageName}-test npm run lint"
    }

    stage('Integration Tests'){
        sh "docker run --rm ${imageName}-test npm run test"
    }

}
