pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                deleteDir()                               
                // setup additional environment              
                // setup the workspace
                // Clone this repository & Parabank repository into the workspace
                bat  '''          
                    git clone https://github.com/dparasoft/parabank.git && cd parabank && ls -ll
                    '''
                // Prepare the jtestcli.properties file

                // Setup soatestcli.properties file
            }
        }
        stage('Jtest: Quality Scan') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for SA
                bat '''
                    cd parabank && mvn -ntp compile jtest:jtest
                    '''
            }
        }
        stage('Jtest: Unit Test') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for Unit Test
                bat '''
                    cd parabank && mvn -ntp compile jtest:agent test jtest:jtest -Djtest.config='builtin://Unit Tests' -Dmaven.test.failure.ignore=true
                    '''
            }
        }
    }
}
