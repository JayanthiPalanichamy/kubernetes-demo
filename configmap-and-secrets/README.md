### ConfigMap and Secrets.


- Consider the code 

```var http = require('http');
   var server = http.createServer(function (request, response) {
     const language = process.env.LANGUAGE;
     const API_KEY = process.env.API_KEY;
     response.write(`Language: ${language}\n`);
     response.write(`API Key: ${API_KEY}\n`);
     response.end(`\n`);
   });
   server.listen(3000);
```

You can define the environment variable in the docker file or in kubernetes yaml.
The shortfall of Docker and Kubernetes environment variables is that they are tied to the container or deployment. If you want to change them, you have to rebuild the container or modify the deployment. Even worse, if you want to use the variable with multiple containers or deployments, you have to duplicate the data!

- To create Kubernetes secret
`kubectl create secret generic apikey --from-literal=API_KEY=123–456`

- To create Configmap
`kubectl create configmap language --from-literal=LANGUAGE=English`
