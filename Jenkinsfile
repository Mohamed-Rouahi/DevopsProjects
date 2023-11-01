pipeline {
    agent any
    stages {
        stage('Set Java Version') {
            steps {
                script {
                    // Set the default JAVA_HOME to Java 8
                    tool name: 'JAVAA_HOME', type: 'jdk'
                }
            }
        }
        stage('Checkout Backend Repo') {
            steps {
                script {
                    // Checkout your source code from the repository.
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
                // Use Java 8 for this stage
                withEnv(["JAVA_HOME=${tool name: 'JAVAA_HOME', type: 'jdk'}"]) {
                    sh 'mvn clean install'
                }
            }
        }
        // stage("SonarQube Analysis") {
        //     steps {
        //         // Set Java 11 for this stage
        //         tool name: 'JAVA_HOME', type: 'jdk'
        //         withEnv(["JAVA_HOME=${tool name: 'JAVA_HOME', type: 'jdk'}"]) {
        //             withSonarQubeEnv('sonarQube') {
        //                 script {
        //                     def scannerHome = tool 'SonarQubeScanner'
        //                     withEnv(["PATH+SCANNER=${scannerHome}/bin"]) {
        //                         sh '''
        //                             mvn sonar:sonar \
        //                                 -Dsonar.java.binaries=target/classes
        //                         '''
        //                     }
        //                 }
        //             }
        //         }
        //     }
        // }
        // stage('Checkout Frontend Repo') {
        //     steps {
        //         script {
        //             // Checkout the frontend repository
        //             checkout([
        //                 $class: 'GitSCM',
        //                 branches: [[name: 'master']], 
        //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/Project-devops-frontend.git']]
        //             ])
        //         }
        //     }
        // }
        // stage('Build Frontend') {
        //     steps {
        //         // Set the Node.js tool defined in Jenkins configuration
        //         script {
        //             def nodeJSHome = tool name: 'nodejs' // Use the correct tool name
        //             env.PATH = "${nodeJSHome}/bin:${env.PATH}"
        //         }
        //         // Now you can run 'npm install' and 'ng build'
        //         sh 'npm install'
        //         sh 'npm run ng build'
        //     }
        // }
        // stage('Build and Push back Images') {
        //     steps {
        //         script {
        //             // Ajoutez l'étape Git checkout pour le référentiel backend ici
        //             checkout([
        //                 $class: 'GitSCM',
        //                 branches: [[name: '*/master']],
        //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
        //             ])

        //             // Build the backend Docker image
        //             def backendImage = docker.build('medrouahi/springapplication', '-f /var/lib/jenkins/workspace/Project-devops/Dockerfile .')

        //             // Authentification Docker Hub avec des informations d'identification secrètes
        //             withCredentials([string(credentialsId: 'docker', variable: 'pwd')]) {
        //                 sh "docker login -u medrouahi -p ${pwd}"
        //                 // Poussez l'image Docker
        //                 backendImage.push()
        //             }
        //         }
        //     }
        // }
        // stage('Build and Push front Image') {
        //     steps {
        //         script {
        //             // Ajoutez l'étape Git checkout pour le référentiel backend ici
        //             checkout([
        //                 $class: 'GitSCM',
        //                 branches: [[name: '*/master']],
        //                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/Project-devops-frontend.git']]
        //             ])

        //             // Build the front Docker image
        //             def frontImage = docker.build('medrouahi/devopsbackend:front', '-f /var/lib/jenkins/workspace/Project-devops/Dockerfile .')

        //             // Authentification Docker Hub avec des informations d'identification secrètes
        //             withCredentials([string(credentialsId: 'docker', variable: 'pwd')]) {
        //                 sh "docker login -u medrouahi -p ${pwd}"
        //                 // Poussez l'image Docker
        //                 frontImage.push()
        //             }
        //         }
        //     }
        // }
       // stage('Deploy to Nexus Repository') {
       //      steps {
                
            
       //        script {
       //                  // Add the Git checkout step for the backend repository here
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



        
         stage('Run Docker Compose') {
     steps {
         script {
             checkout([
                 $class: 'GitSCM',
                 branches: [[name: '*/master']], 
                 userRemoteConfigs: [[url: 'https://github.com/Mohamed-Rouahi/DevopsProjects.git']]
             ])

             // Run the docker-compose command
             sh 'docker compose up -d' 
         }
     }
 }
    }
    post {
        success {
            emailext(
                subject: "Success: SonarQube Analysis Completed",
                body: "SonarQube analysis was successful.",
                to: "mohamed.rouahi@esprit.tn"
            )
        }
        failure {
            emailext(
                subject: "Failure: SonarQube Analysis Failed",
                body: "SonarQube analysis has failed.",
                to: "mohamed.rouahi@esprit.tn"
            )
        }
    }
}
