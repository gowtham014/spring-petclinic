pipeline{
    agent any
    stages{
        stage('vc'){
            git url:"https://github.com/GOWTHI143/spring-petclinic.git",
                branch: "main"
        }
        stage('build image'){
            steps{
                sh"docker image build -t spc:1.0 ."
            }
        }
    }
}