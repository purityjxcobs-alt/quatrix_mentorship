node {
    stage('Execute SSH Deployment & Statistics') {
        // This forces Jenkins to log into test.traccar and pass the code as a stream
        sh '''#!/bin/bash
        ssh -o StrictHostKeyChecking=no user@test.traccar << 'EOF'
            INITIALS="PJ"
            SERVER_TIME=$(date +"%Y-%m-%d %H%M hrs")
            FILE_TIME=$(date +"%Y%m%d-%H%M%S")

            VERSION_INFO=$(cat /etc/os-release | grep VERSION= | cut -d\\( -f2 | cut -d\\) -f1 | tr -d \\")
            VERSION_NUMBER=$(cat /etc/os-release | grep VERSION_ID= | cut -d= -f2 | tr -d \\")
            KERNEL_INFO=$(uname -s -n -r -m)

            REPORT_FILE="/tmp/${INITIALS}-${FILE_TIME}.txt"

            echo "Branch: ${BRANCH_NAME}" > "$REPORT_FILE"
            echo "Status: Build Successful" >> "$REPORT_FILE"
            echo "Time: ${SERVER_TIME}" >> "$REPORT_FILE"
            echo "Server Version: Debian ${VERSION_NUMBER} - ${VERSION_INFO^}" >> "$REPORT_FILE"
            echo "Server Kernel: ${KERNEL_INFO}" >> "$REPORT_FILE"
            
            echo "Verification file successfully generated on test.traccar at: ${REPORT_FILE}"
EOF
        '''
    }
}


