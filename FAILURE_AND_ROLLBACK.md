\# Failure and Rollback



\## 1. Faulty Production Deployment



\### Detection

A faulty deployment can be detected through Kubernetes pod status, readiness/liveness probe failures, application logs, and failed application requests.



\### Recovery / Rollback

First check the deployment and pod status. If the new application version is faulty, roll back the Kubernetes Deployment to the previous working revision.



Example:



kubectl rollout history deployment/todo-summary-assistant



kubectl rollout undo deployment/todo-summary-assistant



After rollback, verify:



kubectl rollout status deployment/todo-summary-assistant



kubectl get pods



The previous working application version should become active again.



\---



\## 2. Application Crashes



\### Detection

Application crashes can be detected using Kubernetes pod status, restart counts, liveness probe failures, and application logs.



Commands that can be used include:



kubectl get pods



kubectl logs <pod-name>



kubectl describe pod <pod-name>



\### Recovery

If the application container crashes, Kubernetes can restart the container automatically. If the problem is caused by a faulty application version, identify the faulty version and roll back to the previous known-good version.



\---



\## 3. Jenkins Is Unavailable



\### Detection

A Jenkins failure can be detected when the Jenkins server or Jenkins job cannot be accessed or a CI build cannot start.



\### Recovery

Application deployment should not depend on Jenkins being continuously available. The source code and deployment state remain in Git. Jenkins can be restarted or repaired and the pipeline can be executed again after Jenkins becomes available.



The Kubernetes environment continues running the currently deployed version while Jenkins is unavailable.



\---



\## 4. Secret Is Leaked



\### Detection

A leaked secret should be treated as compromised immediately. The affected secret must be identified and removed from source code, logs, or other exposed locations.



\### Recovery

Immediately revoke or rotate the compromised credential.



Update the secret in the appropriate secret-management mechanism and redeploy/restart the affected application if required.



Secrets must not be committed to Git.



The Kubernetes Secret manifest containing real credentials should remain excluded from Git.



\---



\## 5. Kubernetes Node Failure



\### Detection

A node failure can be detected using:



kubectl get nodes



and by checking pod status.



A failed node may show a status other than Ready.



\### Recovery

Kubernetes can reschedule workloads onto an available node when the cluster has another suitable node.



The application uses multiple replicas so that availability can be maintained when possible.



After the node is recovered or replaced, verify:



kubectl get nodes



kubectl get pods



and confirm that the application pods are running normally.



\---



\## Rollback Strategy



The deployment uses versioned application images so that a known-good application version can be selected when a faulty version is detected.



Git is the source of truth for deployment configuration. A faulty GitOps change can be rolled back by reverting the Git commit that introduced the faulty deployment state.



Before considering a rollback complete, verify the Kubernetes rollout status, pod health, application logs, and application availability.

