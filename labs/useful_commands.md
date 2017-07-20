## Useful Commands
### Get information about all running pods

	kubectl get pod
	
### Describe one pod

	kubectl describe pop <pop>
	
### Expose the port of a pod (creates a new service)

	kubectl expose pod <pod> --port=444 --name=frontend
	
### Port forward the exposed pod port to your local machine

	kubectl port-forward <pod> 8080
	
### Attach to the pop

	kubectl attach <podname> -i

### Execute a command on the pod

	kubectl exec <pod> -- command


### Add a new label to a pod

	kubectl label pods <pod> mylabel=awesome
	
### Run a shell in a pod (very useful for debugging)

	kubectl run -i --tty busybox --image=busybox --restart=Never -- sh	
	