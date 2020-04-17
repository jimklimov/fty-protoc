pipeline {
    agent { label "devel-image && x86_64 && OSIMAGE_DISTRO=Debian_10.0" }

    parameters {
        booleanParam name: 'RUN_TESTS', defaultValue: true, description: 'Run Tests?'
    }

    stages {
        stage('Build') {
            steps {
                cmakeBuild buildType: 'Release', cleanBuild: true, installation: 'InSearchPath', steps: [[withCmake: true]]
            }
        }

        stage('Test') {
            when {
                environment name: 'RUN_TESTS', value: 'true'
            }
            steps {
                ctest 'InSearchPath'
            }
        }
    }
}
