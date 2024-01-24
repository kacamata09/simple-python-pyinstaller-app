pipeline {
    agent {
        docker {
            image 'python:alpine3.19'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') { 
            steps {
                sh 'chmod o+w ~/.local'
                sh 'pip install pytest'
                sh 'pytest --junit-xml test-reports/results.xml sources/test_calc.py'
            }
        }

    }
}

// node {
//     environment {
//         PATH = "/usr/local/bin/python3"
//     } 

//     docker.image('python:alpine3.19').withRun('-p 3000:3000') {

//         // stage('Debugging') {
//         //     sh 'which python'
//         // }
        
//         stage('Build') {
//             sh 'python3 -m py_compile sources/add2vals.py sources/calc.py' 
//             stash name: 'compiled-results', includes: 'sources/*.py*'
//         }
        
//         stage('Test') {
//             sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//     }
// }
