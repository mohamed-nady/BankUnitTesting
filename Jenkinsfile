pipeline {
    agent {
		node {
			label "master"
			customWorkspace "C:\\Jenkins\\workspaces\\asp.net-example-scmpipeline"
		}
	}
    stages {
        stage('Build') {
            steps {
                bat "C:\\Tools\\nuget\\nuget.exe restore"
				bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\MSBuild\\15.0\\Bin\\MSBuild.exe" Bank\\Bank.csproj'
				bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\MSBuild\\15.0\\Bin\\MSBuild.exe" BankTest\\BankTest.csproj'

            }
        }
        stage('Test') {
            steps {
				bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\Common7\\IDE\\MSTest.exe" /resultsfile:BankTestFirstRun.trx /noisolation /testcontainer:%WORKSPACE%\\BankTest\\bin\\Debug\\BankTest.dll'
				bat '"C:\\Tools\\opencover\\tools\\OpenCover.Console.exe" -register:administrator -target:"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\Common7\\IDE\\MSTest.exe" -targetargs:"/testcontainer:\\"%WORKSPACE%\\BankTest\\bin\\Debug\\BankTest.dll\\" /resultsfile:\\"%WORKSPACE%\\BankTestResults.trx\\"" -mergebyhash -skipautoprops -output:"%WORKSPACE%\\Coverage.xml" -filter:"+[Bank*]* -[BankTest]*"'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello world!' 
            }
        }
    }
}
