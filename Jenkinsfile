pipeline {
    agent any

    stages {
        stage('Execute SSH Deployment & Statistics') {
            steps {
                script {
                    // Running the automated passwordless SSH loopback link to test.traccar
                    sh '''
                        ssh -o StrictHostKeyChecking=no root@test.traccar '
                            # 1. Establish your correct initials (PJ for Purity Jacobs) and server timestamps
                            INITIALS="PJ"
                            SERVER_TIME=$(date +"%Y-%m-%d %H%M hrs")
                            FILE_TIME=$(date +"%Y%m%d-%H%M%S")
                            
                            # 2. Extract operational release specs and Linux kernels
                            VERSION_INFO=$(cat /etc/os-release | grep VERSION= | cut -d\\( -f2 | cut -d\\) -f1 | sed \'s/"//g\')
                            VERSION_NUMBER=$(cat /etc/os-release | grep VERSION_ID= | cut -d= -f2 | sed \'s/"//g\')
                            KERNEL_INFO=$(uname -s -n -r -m)
                            
                            # 3. Formulate the dynamic target report filename path
                            REPORT_FILE="/tmp/${INITIALS}-${FILE_TIME}.txt"
                            
                            # 4. Construct the required verification contents payload
                            echo "Branch: ${BRANCH_NAME}" > $REPORT_FILE
                            echo "Status: Build Successful" >> $REPORT_FILE
                            echo "Time: ${SERVER_TIME}" >> $REPORT_FILE
                            echo "Server Version: Debian ${VERSION_NUMBER} - ${VERSION_INFO^}" >> $REPORT_FILE
                            echo "Server Kernel: ${KERNEL_INFO}" >> $REPORT_FILE
                            
                            echo "Deployment file successfully generated at: ${REPORT_FILE}"
                        '
                    '''
                }
            }
        }
    }
}
