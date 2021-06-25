pipeline{
    agent any
    environment {
       PATH = "/opt/apache-maven-3.8.1/bin:$PATH"
    }
    stages {
        stage("clone code") {
            steps {
                sh 'rm -rf hello-world'
                sh  'git clone https://github.com/hkbonthu7/hello-world.git'
                sh 'pwd'
            }

        }
        stage("clean the code") {
            steps {
                 sh "mvn clean -f hello-world"
                sh 'pwd'
            }
        }
        stage("build the code") {
            steps {
                 sh "mvn install -f hello-world"
                sh 'pwd'
            }
        }
        stage("package the code") {
            steps {
                 sh "mvn package -f hello-world"
                sh 'pwd'
            }
        }
        stage("deploy") {
            steps {
            sshagent(['deploy_user'])  {
                sh 'pwd'
                sh "scp -o StrictHostKeyChecking=no hello-world/webapp1/target/webapp1.war ubuntu@3.235.151.34:/opt/tomcat/apache-tomcat-8.5.68/webapps"
    
}
            }
        }
    }
}
