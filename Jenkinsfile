node {
	stage "Checkout App code"

	checkoutAppCode()


}

def checkoutAppCode() {
	echo "Checkout code here..."
}

def createAWSStack() {
	echo $(ls -l)
	ansible-playbook cfstack-play.yml
}