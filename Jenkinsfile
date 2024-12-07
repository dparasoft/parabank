pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                deleteDir()                               
                // setup additional environment              
                // setup the workspace
                bat  '''          
                    # Clone this repository & Parabank repository into the workspace
                    mkdir parabank
                    git clone https://github.com/dparasoft/parabank.git parabank

                    # Debugging
                    #pwd
                    #ls -ll
                    '''
                // Prepare the jtestcli.properties file

                // Setup soatestcli.properties file
            }
        }
        stage('Jtest: Quality Scan') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the build with Jtest Maven plugin in docker
                bat '''
                    # Compile the project and run Jtest Static Analysis
                    mvn -ntp compile \
                    jtest:jtest \
                    -Djtest.report=./target/jtest/sa \
                    -Djtest.showSettings=true \
                    '''
            }
        }
    }
}
