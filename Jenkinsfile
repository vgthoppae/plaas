node {
	stage "Checkout Pipeline code"

  checkoutPipelineCode()
  echoCurrentDirAndContents('.')

  stage "Checkout App code"
	checkoutAppCode()
	echoCurrentDirAndContents('./appcode')

	stage "Create AWS Stack"
	createAWSStack()

}

// def cleanup() {
// 	echo "Clean up the current working directory"
// 	sh 'rm -rf ./*'
// }

def checkoutPipelineCode() {
	echo "Checking out pipeline code..."
	checkout scm
	echo "Pipeline code Checkout completed..."
}

def checkoutAppCode() {
	echo "Checking out app code..."
	checkout ([$class: 'GitSCM', 
    branches: [[name: '*/vt-plaas']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'appcode']], 
    submoduleCfg: [], 
    userRemoteConfigs: [[url: 'https://github.com/vgthoppae/plaas-cheddar-app.git']]
])
	echo "App code Checkout completed..."
}

def echoCurrentDirAndContents(dir) {
	dirlist = sh (
		script: 'ls -l ${dir}',
		returnStdout: true)
	currentdir = sh (
		script: 'pwd',
		returnStdout: true)

	echo "$dirlist"
	echo "$currentdir"
}

def createAWSStack() {
	
	// sh 'ansible-playbook cfstack-play.yml ../appcode/deployment/params.yml'
}