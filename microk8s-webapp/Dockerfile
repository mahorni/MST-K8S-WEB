FROM nginx:alpine 

COPY index.html.template /usr/share/nginx/html/index.html.template 

COPY default.conf /etc/nginx/conf.d/default.conf 

RUN apk add --no-cache gettext 

CMD envsubst '$POD_NAME $NODE_NAME' < /usr/share/nginx/html/index.html.template > /usr/share/nginx/html/index.html && nginx -g 'daemon off;' 

 

Hjemme side html side. 
cisco@pvl-web-srv-01:~/Documents$ cat index.html.template 

<!DOCTYPE html> 
<html lang="en"> 
<head> 
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <title>Pod og Node Information</title> 
    <style> 
        body { 
            font-family: 'Arial', sans-serif; 
            background-color: #f0f0f0; 
            text-align: center; 
            padding: 50px; 
        } 
        .container { 
            background-color: #ffffff; 
            box-shadow: 0 0 10px rgba(0,0,0,0.1); 
            padding: 20px; 
            margin: 0 auto; 
            width: 80%; 
            max-width: 600px; 
        } 
        h1 { 
            color: #333; 
        } 
        p { 
            color: #666; 
        } 
        .info { 
            background-color: #e9e9e9; 
            padding: 10px; 
            margin: 20px 0; 
            border-radius: 5px; 
        } 
    </style> 

</head> 
<body> 
    <div class="container"> 
        <h1>Velkommen til vores Webside!</h1> 
        <p>Dette er en simpel webside der viser, hvilken Kubernetes pod og node denne side kører på.</p> 
        <div class="info"> 
            <p><strong>Pod Navn:</strong> ${POD_NAME}</p> 
            <p><strong>Node Navn:</strong> ${NODE_NAME}</p> 
        </div> 
    </div>  

 

</body> 
</html>  

Service file 
 

cisco@pvl-web-srv-01:~/Documents$ cat nginx-service.yaml 
apiVersion: v1 
kind: Service 
metadata: 
  name: nginx-service 
spec: 
  selector: 
    app: nginx 
  ports: 
    - protocol: TCP 
      port: 80 
      targetPort: 80 
  type: LoadBalancer 
