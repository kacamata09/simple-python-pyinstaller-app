// pipeline {
//     agent {
//         docker {
//             image 'python:alpine3.19'
//             args '-p 3000:3000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
//                 stash(name: 'compiled-results', includes: 'sources/*.py*')
//             }
//         }
//         stage('Test') { 
//             steps {
//                 sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//             }
//         }

//     }
// }

node {
    docker.image('python:alpine3.19').withRun('-p 3000:3000') {
        
        stage('Build') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
            stash name: 'compiled-results', includes: 'sources/*.py*'
        }
        
        stage('Test') {
            sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
        }
    }
}
