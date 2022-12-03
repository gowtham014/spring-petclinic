pipeline{
    agent any
    stages{
        stage('build image'){
            steps{
                sh"docker image build -t spc:1.0 ."
            }
        }
    }
}