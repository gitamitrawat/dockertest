pipeline
{
	

	environment 
	{
		registry = 'asramitsinghrawat/dockerdemo'
		registryCredential = 'docker-hub'
	}
	
	agent any
	
	stages
	{	
			
				
				stage('docker run') 
				{
					steps
					{	
						notify('started')
						bat "docker run -d --rm -p 8087:8080 --name dockerdemo asramitsinghrawat/dockerdemo:27"	
						notify('Paused')
					}
				}
				
				
				stage('docker stop and remove image') 
				{
					input {
						message "Proceed to stop the container and remove image"
						ok "Yes, Stop it"
					}
					
					steps
					{
						bat "docker stop dockerdemo"
						bat "docker rmi asramitsinghrawat/dockerdemo:27"
					}
				}
	}

	post
	{
		success
		{
			notify('succeded')
		}
		failure
		{
			notify('error')
		}
	}


}

def notify(status)
{
	emailext(to: "asr.amitsinghrawat@gmail.com",
	subject: "${status}: Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]'",
	body:"""<p>${status}: Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]':</p>
	<p>Check Console Output at <a href='${env.BUILD_URL}'>${env.JOB_NAME}[${env.BUILD_NUMBER}]</a></p>"""
	)
}