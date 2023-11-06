pipeline {
    agent any
    stages {
       // stage('Set Java Version') {
         //   steps {
           //     script {
                    // Set the default JAVA_HOME to Java 8
             //       tool name: 'JAVAA_HOME', type: 'jdk'
               // }
            //}
        //}
        stage('Checkout Backend Repo') {
            steps {
                script {
                     Checkout your source code from the repository.
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/master']], 
                        userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
                     ])
                 }
             }
         }
        stage('BUILD Backend') {
            steps {
                
                withEnv(["JAVA_HOME=${tool name: 'JAVAA_HOME', type: 'jdk'}"]) {
                    sh 'mvn clean install'
                }
            }
        }
        stage("SonarQube Analysis") {
           steps {
                
               tool name: 'JAVA_HOME', type: 'jdk'
               withEnv(["JAVA_HOME=${tool name: 'JAVA_HOME', type: 'jdk'}"]) {
                   withSonarQubeEnv('sonarQube') {
                       sh 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage('Checkout Frontend Repo') {
            steps {
                script {
                     
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'master']], 
                        userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/devops-frontend.git']]
                    ])
                }
            }
        }
        stage('Build Frontend') {
            steps {
                 
                script {
                    def nodeJSHome = tool name: 'nodejs' 
                    env.PATH = "${nodeJSHome}/bin:${env.PATH}"
                }
                 
                sh 'npm install'
                sh 'npm run ng build'
            }
        }
        // stage('Build and Push back Images') {
        //     steps {
        //         script {
        //             
        //             checkout([
        //                 $class: 'GitSCM',
        //                 branches: [[name: '*/master']],
        //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
        //             ])

                     
        //             def backendImage = docker.build('medrouahi/springapplication', '-f /var/lib/jenkins/workspace/Project-devops/Dockerfile .')

        
        //             withCredentials([string(credentialsId: 'docker', variable: 'pwd')]) {
        //                 sh "docker login -u medrouahi -p ${pwd}"
        
        //                 backendImage.push()
        //             }
        //         }
        //     }
        // }
        // stage('Build and Push front Image') {
        //     steps {
        //         script {
        
        //             checkout([
        //                 $class: 'GitSCM',
        //                 branches: [[name: '*/master']],
        //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/devops-frontend.git']]
        //             ])


        //             def frontImage = docker.build('medrouahi/angularapp', '-f /var/lib/jenkins/workspace/Project-devops/Dockerfile .')

        
        //             withCredentials([string(credentialsId: 'docker', variable: 'pwd')]) {
        //                 sh "docker login -u medrouahi -p ${pwd}"
       
        //                 frontImage.push()
        //             }
        //         }
        //     }
        // }
        // stage('Deploy to Nexus Repository') {
        //      steps {
                
            
        //        script {
        //                  checkout([
        //                      $class: 'GitSCM',
        //                      branches: [[name: '*/master']],
        //                      userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
        //                  ])
                        
        //                  withCredentials([usernamePassword(credentialsId: 'nexus-credentiel', passwordVariable: 'pwd', usernameVariable: 'name')]) {
        //                      withEnv(["JAVA_HOME=${tool name: 'JAVAA_HOME', type: 'jdk'}"]) {
        //          sh "mvn deploy -s /usr/share/maven/conf/settings.xml -Dusername=\$name -Dpassword=\$pwd"
        //      }
        //     }
        //    }
        //  }
        //  }



        
 //         stage('Run Docker Compose') {
 //     steps {
 //         script {
 //             checkout([
 //                 $class: 'GitSCM',
 //                 branches: [[name: '*/master']], 
 //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
 //             ])

 //             sh 'docker compose up -d' 
 //         }
 //     }
 // }
    }
    post {
        success {
            emailext(
                subject: "Success: Devosps pipeline Completed",
                body: "Devosps pipeline was successful.",
                to: "mohamed.rouahi@esprit.tn"
            )
        }
        failure {
            emailext(
                subject: "Failure: Devosps pipeline Failed",
                body: "Devosps pipeline has failed.",
                to: "mohamed.rouahi@esprit.tn"
            )
        }
    }
}
