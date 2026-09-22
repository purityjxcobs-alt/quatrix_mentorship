        stage('Execute SSH Deployment & Statistics') {
            steps {
                script {
                    def branchName = env.RAW_BRANCH.contains('/') ? env.RAW_BRANCH.substring(env.RAW_BRANCH.lastIndexOf('/') + 1) : env.RAW_BRANCH
                    
                    sshagent(credentials: ['traccar-ssh-key']) {
                        sh """#!/bin/bash
                        # --- FIXED: Changed from 127.0.0.1 to your private Traccar IP ---
                        ssh -o StrictHostKeyChecking=no pkinoti@10.15.0.23 << 'EOF'
                        INITIALS="PJ"
                        SERVER_TIME=\$(date "+%Y-%m-%d %H%M hrs")
                        FILE_TIME=\$(date "+%Y%m%d-%H%M%S")
                        
                        VERSION_INFO=\$(cat /etc/os-release | grep VERSION= | cut -d'(' -f2 | cut -d')' -f1 | tr -d ' ')
                        VERSION_NUMBER=\$(cat /etc/os-release | grep VERSION_ID= | cut -d= -f2 | tr -d ' ')
                        KERNEL_INFO=\$(uname -s -n -r -m)
                        
                        REPORT_FILE="/tmp/\${INITIALS}-\${FILE_TIME}.txt"
                        
                        echo "Branch: ${branchName}" > \$REPORT_FILE
                        echo "Status: Build Passed" >> \$REPORT_FILE
                        echo "Time: \${SERVER_TIME}" >> \$REPORT_FILE
                        echo "Server Version: Debian \${VERSION_NUMBER} - \${VERSION_INFO}" >> \$REPORT_FILE
                        echo "Server Kernel: \${KERNEL_INFO}" >> \$REPORT_FILE
                        
                        echo "=== VERIFICATION FILE LOGS ==="
                        cat \$REPORT_FILE
                        echo "=============================="
                        exit
EOF
                        """
                    }
                }
            }
        }
