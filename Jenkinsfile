pipeline {
    agent{label''}
    stages{
        stage('vcs') {
            steps {
                mail subject: 'Build Started',
                     body: 'Build Started',
                     to: 'boggarapusaigowtham@gmail.com',
                git url: "https://github.com/GOWTHI143/spring-petclinic.git",
                    branch: "task"
            }
        }
        stage('Jfrog package build') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "JFROG2023",
                    releaseRepo: "gowtham-libs-release-local",
                    snapshotRepo: "gowtham-libs-snapshot-local"
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: "MAVEN_TOOL", // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'package',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "JFROG2023"
                )
            }
         }
        stage ('Build docker image') {
            steps {
                mail subject: 'Docker stage',
                     body: 'docker image build started',
                     to: 'boggarapusaigowtham@gmail.com',
                sh """docker image build -t gowtham143.jfrog.io/gowtham-docker/spc:1.0 .
                      docker push gowtham143.jfrog.io/gowtham-docker/spc:1.0"""
                // script {
                //     docker.build('gowtham-docker-local/spc:1.0', "-f Dockerfile .")
                // }
            }
        }
        // stage ('Push image to Artifactory') {
        //     steps {
        //         rtDockerPush(
        //             serverId: "ARTIFACTORY_SERVER",
        //             image: ARTIFACTORY_DOCKER_REGISTRY + '/hello-world:latest',
        //             // Host:
        //             // On OSX: "tcp://127.0.0.1:1234"
        //             // On Linux can be omitted or null
        //             host: HOST_NAME,
        //             targetRepo: 'docker-local',
        //             // Attach custom properties to the published artifacts:
        //             properties: 'project-name=docker1;status=stable'
        //         )
        //     }
        // }
    }
    post {
         success{
                mail subject: 'Build success',
                     body: 'Build success',
                     to: 'boggarapusaigowtham@gmail.com'
            }
            failure {
            mail subject: 'Build Failed',
                  body: 'Build Failed',
                  to: 'boggarapusaigowtham@gmail.com'
            }
        }
}
