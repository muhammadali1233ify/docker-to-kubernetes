# docker-to-kubernetes
## Description

## Procedure
1. Once the cluster is intanciated, follow the access guideline of the service from page.

2. Pull a docker image of your choice. Typically all images come with a dockerfile that describe the environment and the necessary files required for running that instance.
'docker pull nshou/elasticsearch-kibana'

3. Tag your release to explicitly identify it with IBM registry url that you intanciated your cluster on. In our case it's 'us-east'. The namespace below is 'wsa-namespace' and image name and tag is defined as 'nshou-elastic-kibana:0.1'.
'docker tag nshou/elasticsearch-kibana registry.us-east.bluemix.net/wsa-namespace/nshou-elastic-kibana:0.1'
 
4. Push the new release on ibmcloud. The image can then be found on cloud registry and can be viewed using 'ibmcloud cr image-list'
'docker push registry.us-east.bluemix.net/wsa-namespace/nshou-elastic-kibana:0.1'
 
5. build your deployment image. All the deployment should be written as a '**Dockerfile** with all the dependencies in it. Exposed ports in this docker deployment are 9200 and 5601
'ibmcloud cr build -t registry.ng.bluemix.net/wsa-namespace/nshou-elastic-kibana:0.1 .'
 
6. create deployment and service using **.yml** file. NodePort definition is optional as the kubernetes engine will automatically define it.
kubectl create -f nshou-elastic-kibana-deploy-yml.yml
 
7. Your application will hosted at <cluster_IP_address>:<NodePort>
'http://169.63.76.233:30007'
