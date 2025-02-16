pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    parameters {
        string defaultValue: 'testng.xml', name: 'xml_file', description: 'TestNG XML file'
        string defaultValue: 'chrome', name: 'browser', description: 'Browser (chrome, firefox, edge, headless)'
        booleanParam defaultValue: true, name: 'headless', description: 'Run in headless mode?'
    }
    stages {
        stage('Run Tests') {
            steps {
                script {
                    def xmlFile = params.xml_file
                    def browser = params.browser
                    def headless = params.headless ? 'true' : 'false'

                    sh """
                        mvn clean test \
                            -DsuiteFile=${xmlFile} \
                            -Dbrowser=${browser} \
                            -Dheadless=${headless} \
                            -e
                    """
                }
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
        }
    }
}