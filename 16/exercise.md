Description: There's a k3s Kubernetes install you can access with kubectl. The Kubernetes YAML manifests under /home/admin have been applied. The objective is to access from the host the "webapp" web server deployed and find what message it serves (it's a name of a town or city btw). In order to pass the check, the webapp Docker container should not be run separately outside Kubernetes as a shortcut.

Test: curl localhost:8888 returns a value from the webapp deployed Kubernetes pod.
