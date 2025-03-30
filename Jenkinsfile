// Defines the pipeline structure
pipeline {
    // Specifies where the pipeline will run - 'any' available agent
    agent any

    // Define options for the pipeline
    options {
        // Skip the default SCM checkout by Jenkins, as GitHub Actions already handles it
        skipDefaultCheckout()
        // Add timestamps to console output
        timestamps()
    }

    // Define the stages of the pipeline
    stages {
        // Stage 1: Simple setup or verification (optional but good practice)
        stage('Setup Environment') {
            steps {
                // Run shell commands within steps
                script {
                    echo "Verifying Java and Gradle versions..."
                    // Use sh for Linux runners in GitHub Actions
                    sh 'java -version'
                    // Make gradlew executable (important on Linux runners)
                    sh 'chmod +x ./gradlew'
                    sh './gradlew --version'
                }
            }
        }

        // Stage 2: Build the application using Gradle wrapper
        stage('Build') {
            steps {
                echo "Running Gradle assemble..."
                // Use ./gradlew to ensure the project's specified Gradle version is used
                // This matches the task requirement
                sh './gradlew assemble'
            }
        }

        // Stage 3: Run the unit tests using Gradle wrapper
        stage('Test') {
            steps {
                echo "Running Gradle test..."
                // This matches the task requirement
                sh './gradlew test'
            }
        }
    }

    // Define actions that run after the pipeline finishes, regardless of status
    post {
        always {
            echo 'Pipeline finished.'
            // Clean up Gradle build artifacts (optional)
            // cleanWs()
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}