pipeline {
    agent any
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN"
    }
    stages {
        stage("version of software"){
            steps{
                sh "mvn --version"
            }
        }
        stage("clean old build file"){
            steps{
                sh "mvn clean"
            }
        }
        stage("compile maven project"){
            steps{
                sh "mvn compile"
            }
        }
        stage("test the project"){
            steps{
                sh "mvn test"
            }
        }
        stage("create the jar or war"){
            steps{
                sh "mvn package"
            }
        }
         stage("creating the image"){
            steps{
                sh "docker build -t my-spring-app . -f Dockerfile"
                echo "image created"
            }
        }
        stage("run the container"){
            steps{
                sh "docker run -d -p 9090:9090 my-spring-app"
                echo "container running"
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'Example : if the Pipeline was previously failing but is now successful'
        }
    }
}
