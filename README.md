This is Selenium based project to run test cases with Selenium grid running inside Docker containers over a Kubernetes cluster.

Created a single node cluster using Minikube. Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node. We can start the cluster with docker driver, which will create VM inside a docker container.

Once cluster is ready, we can start creating pods, kubenetes services, replication controller, HPA, namespace using yml files.

We can use NodePort or LoadBalancer to expose the outside traffic in VM to access the cluster from Selenium script where we have used RemoteWebDriver to access this URL. We will access the Kubenetes service from outside rather than Selenium Hub, which will control the entire setup of selenium grid.

If we need multi node cluster then we can use KIND(Kubernetes in Docker) to setup the cluster.

In case you get ImagePullBackOff error in Pod status due to size of selenium browser docker images then you can first pull the image before creating pod using "minikube image pull selenium/hub:4.0.0".

We can autoscale pods depends on utilization:

kubectl autoscale rc selenium-node-chrome --min=3  --max=5 --cpu-percent=80
kubectl autoscale rc selenium-node-firefox --min=3  --max=5 --cpu-percent=70



