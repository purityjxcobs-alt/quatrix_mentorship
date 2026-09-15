pipeline {
    agent any

    environment {
        // Change these initials to your own name initials
        INITIALS = "KK" 
        SSH_CRED_ID = "traccar-ssh-key"
        // Update this to the actual domain or IP of your test.traccar server
        TARGET_SERVER = "test.traccar" 
    }

    stages {
        define_env {
            stage('Checkout') {
                steps {
                    checkout scm
                }
            }
        }
    }

    post {
        always {
            // This block executes regardless of build success or failure
            sshagent(credentials: [env.SSH_CRED_ID]) {
                script {
                    // Determine status text based on current build result
                    def buildStatus = currentBuild.currentResult == 'SUCCESS' ? 'Build Passed' : 'Build Failed'
                    
                    // Construct the SSH commands to extract target server info and write the file
                    def remoteCommand = """
                        # Get remote server date-time
                        TIMESTAMP=\$(date +'%Y-%m-%d-%H%M%S')
                        FILE_TIME=\$(date +'%Y-%m-%d %H%M hrs')
                        FILENAME="/tmp/${env.INITIALS}-\${TIMESTAMP}.txt"
                        
                        # Fetch Debian system information
                        SERVER_VER=\$(cat /etc/os-release | grep -E '^PRETTY_NAME=' | sed 's/PRETTY_NAME=//' | tr -d '"')
                        SERVER_KERNEL=\$(uname -snr)
                        
                        # Generate file content
                        echo "Branch: ${env.BRANCH_NAME}" > \$FILENAME
                        echo "Status: ${buildStatus}" >> \$FILENAME
                        echo "Time: \${FILE_TIME}" >> \$FILENAME
                        echo "Server Version: \${SERVER_VER}" >> \$FILENAME
                        echo "Server Kernel: \${SERVER_KERNEL}" >> \$FILENAME
                    """
                    
                    // Execute commands safely over SSH disable strict host checking for automation convenience
                    sh "ssh -o StrictHostKeyChecking=no ${env.SSH_CRED_ID} @${env.TARGET_SERVER} \"${remoteCommand}\""
                }
            }
        }
    }
}
