pipeline {
    agent any

    stages {
        stage('Execute SSH Deployment & Statistics') {
            steps {
                script {
                    // Executing the automated passwordless SSH connection straight to test.traccar
                    sh '''
                        ssh -o StrictHostKeyChecking=no root@test.traccar '
                            # 1. Map your correct Purity Jacobs name initials and server timestamps
                            INITIALS="PJ"
                            SERVER_TIME=$(date +"%Y-%m-%d %H%M hrs")
                            FILE_TIME=$(date +"%Y%m%d-%H%M%S")
                            
                            # 2. Extract operational release specs and Linux kernels
                            VERSION_INFO=$(cat /etc/os-release | grep VERSION= | cut -d\\( -f2 | cut -d\\) -f1 | tr -d \\")
                            VERSION_NUMBER=$(cat /etc/os-release | grep VERSION_ID= | cut -d= -f2 | tr -d \\")
                            KERNEL_INFO=$(uname -s -n -r -m)
                            
                            # 3. Establish the destination file path
                            REPORT_FILE="/tmp/${INITIALS}-${FILE_TIME}.txt"
                            
                            # 4. Construct the required contents payload
                            echo "Branch: ${BRANCH_NAME}" > "$REPORT_FILE"
                            echo "Status: Build Successful" >> "$REPORT_FILE"
                            echo "Time: ${SERVER_TIME}" >> "$REPORT_FILE"
                            echo "Server Version: Debian ${VERSION_NUMBER} - ${VERSION_INFO^}" >> "$REPORT_FILE"
                            echo "Server Kernel: ${KERNEL_INFO}" >> "$REPORT_FILE"
                            
                            echo "Verification file successfully generated at: ${REPORT_FILE}"
                        '
                    '''
                }
            }
        }
    }
}

