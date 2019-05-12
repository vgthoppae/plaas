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
	def dirlist = sh 'ls -l'
	echo ${dirlist}
	sh 'ansible-playbook cfstack-play.yml'
}