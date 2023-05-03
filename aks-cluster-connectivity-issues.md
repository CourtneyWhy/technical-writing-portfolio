# Fixing Connectivity Issues with Azure Kubernetes Service (AKS) Clusters

If you're having trouble connecting to your Azure Kubernetes Service (AKS) cluster, issues with the API server, or service and application connectivity, there could be several reasons. These issues might be caused by incorrect cluster configurations, network restrictions, or load balancer misconfigurations. This article provides steps to help identify and resolve common connectivity issues. 

Before starting, make sure you have access to the Azure Portal and have both Azure CLI and kubectl installed on your system.


## Verify your cluster status and configuration

1. Sign in to the Azure portal [Azure portal](https://portal.azure.com) and go to your AKS cluster.
2. Look at the cluster status on the main page. If you see any issues or notifications, address them accordingly.
3. Double-check your Kubernetes version and Node size settings to ensure they are correctly set and that the cluster is running.

## Check network connectivity and firewall rules

1. Verify that your network permits outbound connections to the AKS cluster's API server.
2. Make sure that the appropriate firewall rules are in place, allowing traffic between your network and the AKS cluster.
3. Go to **Network security group** settings in the [Azure portal](https://portal.azure.com) to verify if there are any misconfigurations.

## Validate your load balancer configuration

1. Inspect the load balancer settings associated with your AKS cluster in the [Azure portal](https://portal.azure.com).
2. Confirm that the load balancer is set up correctly to route traffic to your AKS cluster's API server.
3. Check the health probes and backend pool configurations to ensure they are accurate.

## Need more help?

Check the AKS troubleshooting guide to see whether your problem is described there. This article describes additional details and considerations from a network troubleshooting perspective and specific problems that might arise. [AKS troubleshooting guide](https://learn.microsoft.com/en-us/azure/aks/troubleshooting).
