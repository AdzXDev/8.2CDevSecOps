pipeline { 
  agent any 
  stages { 
    stage('Checkout') { 
      steps { 
        echo 'Tool used for Checkout: Git'
        git branch: 'main', url: 'https://github.com/AdzXDev/8.2CDevSecOps.git' 
      } 
    } 
    stage('Install Dependencies') { 
      steps { 
        echo 'Tool used for Build/Install: npm (Node Package Manager)'
        sh 'npm install' 
      } 
    } 
    stage('Run Tests') { 
      steps { 
        echo 'Tool used for Testing: Mocha / Jest'
        sh 'npm test || true' 
      }
      post {
        always {
            emailext(
                subject: "Test Stage Status: ${currentBuild.currentResult}",
                body: "The Run Tests stage completed. Please check the attached logs.",
                to: "adityadhapodkar123@gmail.com",
                attachLog: true
            )
        }
      }
    } 
    stage('Generate Coverage Report') { 
      steps { 
        echo 'Tool used for Coverage: Istanbul / nyc'
        sh 'npm run coverage || true' 
      } 
    } 
    stage('NPM Audit (Security Scan)') { 
      steps { 
        echo 'Tool used for Security Scan: npm audit / Snyk'
        sh 'npm audit || true' 
      }
      post {
        always {
            emailext(
                subject: "Security Scan Status: ${currentBuild.currentResult}",
                body: "The Security Scan stage completed. Please check the attached logs.",
                to: "adityadhapodkar123@gmail.com",
                attachLog: true
            )
        }
      }
    } 
  } 
}