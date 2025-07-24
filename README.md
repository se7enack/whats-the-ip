# ipv4check setup
ipify-like endpoint used for checking public ipv4 ip addresses
###


- edit these files to have the public dns name of ipv4check host
    - docker/nginx.conf
    - ingress/ingress-route.yaml


- edit this file to have the correct ip for the INGRESS_CONTROLLER_IP
    - ingress/create-ipv4check-ingress.sh


- edit docker/nginx.conf to have the correct public FQDN you'll be using for ipv4check 


- log into docker.io and create a repo to host the ipv4check image


- build the docker image and send it to docker.io
  
    ```
    cd docker

    docker login -u {YOUR_USERNAME}

    docker build . -t {YOUR_USERNAME}/{REPONAME}:v1.0

    docker push {YOUR_USERNAME}/{REPONAME}:v1.0
    ```


- update the deployment yaml to point at your new image
  - deployment/ipv4check-deployment.yaml

      example:
      
          image: {YOUR_USERNAME}/{REPONAME}:v1.0


- create k8s name space
    - deploy ipv4check-namespace.yaml
  
          kubectl apply -f ipv4check-namespace.yaml
      
      OR
      

    - run kubectl command

          kubectl create namespace ipv4check
        

- create deployment

      kubectl apply -f deployment/ipv4check-deployment.yaml


- create service

      kubectl apply -f service/ipv4check-service.yaml

        
        
- create ingress

      cd ingress && ./create-ipv4check-ingress.sh

--------------------------------------------------

## example usage

#### plain text:
```
curl -L https://ipv4ip.com


12.34.56.78
```
____


#### json:
```
curl -L https://ipv4ip.com/?format=json


{"ip":"12.34.56.78"}
```
____


#### xml:
```
curl -L https://ipv4ip.com/?format=xml


<ip>12.34.56.78</ip>
```
___


#### yaml:
```
curl -L https://ipv4ip.com/?format=yaml

ip: 12.34.56.78
```
____


Live Example: https://ipv4ip.com

 
