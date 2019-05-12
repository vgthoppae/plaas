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
	echo (sh 'ls -l')
	sh 'ansible-playbook cfstack-play.yml'
}