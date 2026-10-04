\# Monitoring and Operations



\## 1. Application Metrics



Describe the important metrics to monitor:

\- Application availability

\- Response time

\- HTTP error rate

\- CPU usage

\- Memory usage

\- Pod restart count



\## 2. Kubernetes Monitoring



Monitor:

\- Pod status

\- Deployment status

\- Node status

\- CPU and memory utilization

\- Readiness probe failures

\- Liveness probe failures



Useful commands:



kubectl get pods

kubectl get deployments

kubectl get nodes

kubectl describe pod <pod-name>



\## 3. Application Logs



Application logs should be checked when:

\- A pod crashes

\- Requests fail

\- Database connectivity fails

\- Application startup fails



Useful command:



kubectl logs <pod-name>



\## 4. Alerts



Important alerts include:

\- Pod repeatedly restarting

\- Pod not ready

\- Deployment rollout failure

\- High CPU usage

\- High memory usage

\- Increased HTTP errors

\- Kubernetes node becoming unavailable



\## 5. Early Failure Detection



Readiness and liveness probes help detect application problems.



The readiness probe checks whether the application is ready to receive traffic.



The liveness probe checks whether the application is still functioning and allows Kubernetes to restart an unhealthy container.



Resource requests and limits help prevent uncontrolled resource consumption.



\## 6. Operational Checks



Before and after a deployment, verify:



kubectl get pods

kubectl get deployments

kubectl get services

kubectl get nodes



Also check application logs and confirm that the application endpoint responds successfully.

