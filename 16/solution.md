1. Review K8s and pod state for our namespace: kubectl get all -n web , kubectl describe pod -n web

2. The status of the webapp-deployment is ImagePullBackOff. The webapp pod description says: Failed to pull image "webapp". Try and docker pull webapp

3. Check docker images --digests

4. There is a registry image you can use. (Open window once more to see the main solution)

5. Create a registry and push the webapp image to it so a digest is added to the image: docker run -d -p 5000:5000 registry:2 ; docker tag webapp localhost:5000/webapp ; docker push localhost:5000/webapp. Change the deployment manifest so that image: is localhost:5000/webapp (or pull image from the repository and use that) and deploy: kubectl apply -f deployment.yaml (Open window again to see the rest of the solution)

6. Fix in deployment.yaml for the container spec, containerPort: should be 8888 , and redeploy.
Tunnel from the webapp pod to the local :8888 port and curl to it: kubectl port-forward deployments/webapp-deployment 8888 -n web & ; curl localhost:8888 (another option to get the message from the webapp is to kubectl exec into the pod and curl locally but this is not verified by the "Check Solution" script).
