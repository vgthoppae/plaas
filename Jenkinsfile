node {
	echo "App being built is ${AppName}"

	cleanup()

	stage "Checkout Pipeline code"

  checkoutPipelineCode()

	def app = getAppMetadata()
	echo "${app}"
	// echo "${app.name}"
	echo "${app['name']}"
	// echo "${app['gitrepo']}"

 //  // echoCurrentDirAndContents()

 //  stage "Checkout App code"
	// checkoutAppCode()
	// echoCurrentDirAndContents()

	// stage "Create AWS Stack"
	// createAWSStack()

}

def getAppMetadata() {
	def appMetadata = load 'app-metadata/cheddar.groovy'
  def cheddar = "${appMetadata.cheddar}"
  echo "$cheddar"
  // echo "${cheddar.gitrepo}"
  return cheddar
}

def cleanup() {
	echo "Clean up the current working directory"
	sh 'rm -rf ./*'
}

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

def echoCurrentDirAndContents() {
	dirlist = sh (
		script: 'ls -l appcode',
		returnStdout: true)
	currentdir = sh (
		script: 'pwd',
		returnStdout: true)

	echo "$dirlist"
	echo "$currentdir"
}

def createAWSStack() {
	
	sh 'ansible-playbook cfstack-play.yml --extra-vars "@./appcode/deployment/params.yml"'
}