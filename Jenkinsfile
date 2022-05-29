def imageName = 'olivier/movies-store'

node('workers'){
    stage('Checkout'){
        checkout scm
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality Tests'){
        imageTest.inside{
	    sh 'npm run lint'
        }
    }

    stage('Integration Tests'){
        imageTest.inside{
            withEnv(["NODE_PATH=/usr/local/lib/node_modules"]) {
	         sh 'npm run test'
            }
        }
    }

}
