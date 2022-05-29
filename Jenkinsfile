def imageName = 'olivier/movies-store'

node('workers'){
    stage('Checkout'){
        checkout scm
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality Tests'){
        sh "docker run --rm ${imageName}-test npm run lint"
    }

    //stage('Integration Tests'){
    //    imageTest.inside('-u root:root'){
   //         withEnv(["NODE_PATH=/app/node_modules:/usr/local/lib/node_modules"]) {
//	         sh 'npm run test'
 //           }
  //      }
   // }

}
