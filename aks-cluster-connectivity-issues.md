# Fixing Connectivity Issues with Azure Kubernetes Service (AKS) Clusters

If you're having trouble connecting to your Azure Kubernetes Service (AKS) cluster, issues with the API server, or service and application connectivity, there could be several reasons. These issues might be caused by incorrect cluster configurations, network restrictions, or load balancer misconfigurations. This article provides steps to help identify and resolve common connectivity issues. 

Before starting, ensure sure you have access to the Azure Portal and have both Azure CLI and kubectl installed on your system.


## Verify your cluster status and configuration

1. Sign in to the Azure portal [Azure portal](https://portal.azure.com) and go to your AKS cluster.
2. From the search bar, enter **Kubernetes services**, and then select your AKS cluster from the list.
3. In the **Overview** tab, check the Status field. Follow the suggested actions to resolve any status issues or notifications. For help resolving status issues, refer to the [AKS troubleshooting guide](https://learn.microsoft.com/en-us/azure/aks/troubleshooting).
4. From the left menu, under Settings, select **Properties**. Verify your Kubernetes version and Node size settings are correct and that your cluster is running.

If you're still experiencing connectivity issues, proceed to the next section and follow the steps to check your network configuration.


## Check network connectivity and firewall rules

1. From the left menu, under Settings, select **Networking**. Check your cluster's network configuration, ensuring it's set up correctly for your requirements.
2. If you have network policies enabled, ensure they're properly configured to allow traffic to and from the required sources and destinations. To review and edit network policies, select **Network policies** under Settings from the left menu.
3. If you're using a custom VNET, verify that your subnet settings, Network Security Groups (NSGs), and User-Defined Routes (UDRs) are configured correctly. You can find these settings by entering **virtual networks** in the search bar, select the VNET associated with your AKS cluster from the list, and then select **Settings** under VNET in the left menu.
4. If you're using a load balancer, ensure it's correctly configured and associated with the required services. To check load balancer settings, enter **Load balancers** in the search bar, select the appropriate load balancer from the list, and then Select **Settings** from the left menu.
7. After checking and adjusting the network configurations and policies as needed, test your cluster's connectivity again.

If you're still experiencing connectivity issues, proceed to the next section and follow the steps to validate your load balancer configuration.


## Verify that your Kubernetes resources are configured correctly

1. From an elevated command line, run the following command to configure your 'kubectl' to use the credentials for your AKS cluster. Replace `<your-resource-group>` and `<your-cluster-name>` with the appropriate values for your AKS cluster:
```
az aks get-credentials --resource-group <your-resource-group> --name <your-cluster-name>
```
2. Check the status of your cluster's nodes by running the following commandkubectl get nodes
```
kubectl get nodes
```
3. Review the output, ensure all nodes are in the `Ready` state, and then check the status of your cluster's pods by running the following command:
```
kubectl get pods --all-namespaces
```
4. Review the output of the `kubectl get pods --all-namespaces` command and look for any pods with a status other than `Running` or `Completed`. Investigate and resolve any issues with the pods that might be causing connectivity problems.
5. Use the following command to check the logs for any problematic pods to gain insight into the issues. Replace `<namespace>` and `<pod-name>` with the appropriate values:
```
kubectl logs -n <namespace> <pod-name>
```
6. Review the logs for any error messages or signs of misconfiguration. Address any issues you find and retest the connectivity to your AKS cluster.

If you're still experiencing issues after following the steps in this article, check the [AKS troubleshooting guide](https://learn.microsoft.com/en-us/azure/aks/troubleshooting).
