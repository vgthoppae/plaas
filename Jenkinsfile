node {
	stage "Checkout App code"

	checkoutAppCode()

	stage "Create AWS Stack"
	createAWSStack()

}

def checkoutAppCode() {
	echo "Checkout code here..."
	checkout scm
	echo "Checkout completed..."
}

def createAWSStack() {
	dirlist = sh (
		script: 'ls -l',
		returnStdout: true)
	currentdir = sh (
		script: 'pwd',
		returnStdout: true)

	echo "$dirlist"
	echo "$currentdir"
	sh 'ansible-playbook cfstack-play.yml'
}