node {
	stage "Checkout App code"

	checkoutAppCode()

	stage "Create AWS Stack"
	createAWSStack()

}

def checkoutAppCode() {
	echo "Checkout code here..."
}

def createAWSStack() {
	dirlist = sh (
		script: 'ls -l',
		returnStdout: true)

	echo "$dirlist"
	// sh 'ansible-playbook cfstack-play.yml'
}