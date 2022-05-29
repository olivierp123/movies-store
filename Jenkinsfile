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

    stage('Coverage Reports'){
        sh "docker run --rm -v $PWD/coverage:/app/coverage ${imageName}-test npm run coverage-text"
        publishHTML (target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: "$PWD/coverage",
            reportFiles: "index.html",
            reportName: "Coverage Report"
        ])

    }

}
