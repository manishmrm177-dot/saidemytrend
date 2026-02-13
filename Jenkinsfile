pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----------- build completed ----------"
            }
        }

        stage("test") {
            steps {
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test completed ----------"
            }
        }

        stage('SonarQube analysis') {         // 8  // Creates a stage named 'SonarQube analysis'
            environment {                     // 9  // Defines environment variables specific to this stage
                scannerHome = tool 'sonarqube-scanner'  
                                              // Sets the SonarQube scanner tool
            }                                 // 9  // Ends the environment block for this stage

            steps {                           // 10  // Defines the steps that will be executed in this stage
                withSonarQubeEnv('saidemy-sonarqube-server') {
                                              // Executes the SonarQube analysis within the SonarQube environment
                    sh "${scannerHome}/bin/sonar-scanner"  
                                              // Runs the SonarQube scanner tool
                }                             // Ends the withSonarQubeEnv block
            }                                 // 10  // Ends the steps block for 'SonarQube analysis' stage
        }                                     // 8  // Ends the 'SonarQube analysis' stage
    }
}

