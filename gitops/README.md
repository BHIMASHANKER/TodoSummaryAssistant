GitOps Deployment



Purpose

Explain that Kubernetes deployment state is maintained in Git.



CI/CD Flow

1\. Developer pushes application code to GitHub.

2\. Jenkins checks out the code.

3\. Jenkins builds and tests the application.

4\. Jenkins builds and pushes a versioned Docker image.

5\. Kubernetes deployment state is updated through GitOps.

6\. The Kubernetes environment reconciles the desired state.



Deployment Trigger

Explain how a change to the Git-managed Kubernetes state causes the desired application version to be deployed.



Rollback

Explain that a faulty GitOps change can be rolled back by reverting the Git commit containing the bad deployment/image version.



Important Rule

Jenkins does not directly run kubectl apply or otherwise deploy to Kubernetes.

