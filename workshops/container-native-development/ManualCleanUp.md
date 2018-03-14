# Cleaning Up After the Workshop

## Introduction

Now that you have completed the workshop, you may want to remove the artifacts left behind in your Oracle Cloud trial account. This guide will show you how to remove everything that you created during the workshop. Note that compute instances and load balancers left running in your Oracle Cloud trial account will continue to consume trial credits until they are terminated.

**_To log issues_**, click here to go to the [GitHub oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

**Remove All Deployed Workshop Components**

- Clean up Oracle Cloud Account
  - Destroy all Oracle Cloud Infrastructure

# Remove All Deployed and Installed Workshop Components

## Clean up Oracle Cloud Account

### **STEP 1**: Delete Instances

- As documented in the other labs, connect into your Oracle Cloud Account, and go to the Cloud Console.
- From the Cloud Console, select **Compute > Images** from the top menu option

  ![](images/manualcleanup/pic01.png)



- First we need to delete any load balancers created by Kubernetes outside of the Terraform infrastructure we provisioned. From a **terminal window** where you have the `KUBECONFIG` environment variable correctly set, run the following command:

  `kubectl delete svc --all`

- To remove all Terraform-created infrastructure from your Oracle Cloud trial account, we will make use of the `terraform-kubernetes-installer` configuration that you created in Lab 200 of the workshop. In a **terminal window**, navigate to the `terraform-kubernetes-installer` directory (your path may differ):

  `cd ~/terraform-kubernetes-installer`

- Remove all instances, load balancers, and virtual cloud networks from your account with the following command:

  `terraform destroy`

- Type `yes` when prompted to continue with the destroy command.

- Wait while Terraform removes your infrastructure and ensure that no errors occur.

## Clean up Locally Installed Software

### **STEP 2**: Remove Fn

  `rm /usr/local/bin/fn`

### **STEP 3**: Remove Helm and the fn-helm Installer

  `cd ~/Downloads/helm/*/fn-helm && ../helm delete --purge my-release`
  `rm -rf ~/Downloads/helm`

### **STEP 5**: Remove terraform-kubernetes-installer

  **NOTE**: Do not remove this directory until you have successfully destroyed your infrastructure following the instructions in **STEP 1**. Terraform will not be able to automate the destruction of your infrastructure once you delete this directory.

  `rm -rf ~/terraform-kubernetes-installer`

### **STEP 6**: Remove Terraform

  `rm /usr/local/bin/terraform`

### **STEP 7**: Remove OCI API Keys

  **NOTE**: Do not remove this directory until you have successfully destroyed your infrastructure following the instructions in **STEP 1**. Terraform will not be able to automate the destruction of your infrastructure once you delete this directory.

  `rm -rf ~/.oci`

### **STEP 8**: Remove image-resize Function

  `rm -rf ~/image-resize`

### **STEP 9**: Uninstall Docker

  **MacOS**: `/Applications/Docker.app/Contents/MacOS/Docker --uninstall`
  **Linux**:
    `rm -rf /var/lib/docker`
    AND
    `sudo apt-get remove docker docker-engine docker.io`
    OR
    `sudo yum remove docker docker-common docker-selinux docker-engine`