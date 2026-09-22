def runRemoteReport(String branch, String status) {
    sshagent(credentials: ['traccar-ssh-key']) {
        sh """#!/bin/bash
        ssh -o StrictHostKeyChecking=no pkinoti@127.0.0.1 << 'EOF'
        INITIALS="PJ"
        SERVER_TIME=\$(date "+%Y-%m-%d %H%M hrs")
        FILE_TIME=\$(date "+%Y%m%d-%H%M%S")
        
        VERSION_INFO=\$(cat /etc/os-release | grep VERSION= | cut -d'(' -f2 | cut -d')' -f1 | tr -d ' ')
        VERSION_NUMBER=\$(cat /etc/os-release | grep VERSION_ID= | cut -d= -f2 | tr -d ' ')
        KERNEL_INFO=\$(uname -s -n -r -m)
        
        REPORT_FILE="/tmp/\${INITIALS}-\${FILE_TIME}.txt"
        
        echo "Branch: ${branch}" > \$REPORT_FILE
        echo "Status: Build ${status}" >> \$REPORT_FILE
        echo "Time: \${SERVER_TIME}" >> \$REPORT_FILE
        echo "Server Version: Debian \${VERSION_NUMBER} - \${VERSION_INFO}" >> \$REPORT_FILE
        echo "Server Kernel: \${KERNEL_INFO}" >> \$REPORT_FILE
        
        # --- NEW CODE: This prints the file contents directly into your Jenkins log screen ---
        echo "=== VERIFICATION FILE LOGS ==="
        cat \$REPORT_FILE
        echo "=============================="
        
        exit
EOF
        """
    }
}
