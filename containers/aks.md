---
title: Azure Kubernetes Service
description: RCL SSL for Azure Kubernetes 
parent: Containers
nav_order: 4
---

# SSL/TLS for Azure Kubernetes Service (AKS)

In this section, you will learn how to set up SSL/TLS in Azure Kubernetes Service (AKS). The steps are as follows :

- Crate SSL/TLS certificate(s) in the RCL SSL Portal using the [Key Vault](../portal/azure-keyvault.md) or [Key Vault SAN](../portal/azure-keyvault-san.md) option

- Use the NGINX application routing add-on as an ingress controller in your AKS cluster

- Terminate HTTPS traffic in the managed NGINX ingress controller with the TLS/SSL certificate(s) from Azure Key Vault

- Use the [RCL SSL AutoRenew Function](../autorenew/autorenew.md) app to automatically renew certificates in Azure Key Vault before they expire

{: .information }
Before you progress further, you must have already created your certificate(s) in the RCL SSL Portal using the [Azure Key Vault](../portal/azure-keyvault.md) or [Azure Key Vault SAN](../portal/azure-keyvault-san.md) option.

# Install the NGINX Application Routing Add-On in AKS

Follow the instructions in the link to deploy and configure the application routing add-on for the managed NGINX ingress controller

- [NGINX Application Routing Add-On for AKS](https://learn.microsoft.com/en-us/azure/aks/app-routing?tabs=default%2Cdeploy-app-default)

# Terminate HTTPS traffic with certificate(s) from Azure Key Vault

Follow the instruction in the link to terminate HTTPS traffic with certificate(s) from Azure Key Vault

- [Terminate HTTPS traffic with certificate(s) from Azure Key Vault](https://learn.microsoft.com/en-us/azure/aks/app-routing-dns-ssl)

The following deployment file shows a sample set up for SSL/TLS in AKS using Azure Key Vault and the managed NGINX application routing add-on for AKS:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-aspnetapp
  labels:
    deployment: aspnetapp
spec:
  selector:
    matchLabels:
      app: aspnetapp
  replicas: 2
  template:
    metadata:
      labels:
        app: aspnetapp
    spec:
      containers:
      - name: aspnetapp-image
        image: mcr.microsoft.com/dotnet/samples:aspnetapp
        ports:
        - containerPort: 8080
          protocol: TCP

---

apiVersion: v1
kind: Service
metadata:
  name: aspnetapp-service
spec:
  selector:
    app: aspnetapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080

---

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    kubernetes.azure.com/tls-cert-keyvault-uri: https://rclkeyvault.vault.azure.net/certificates/example-com/bf0etgd56g4gd563a969a8c1c7ed6a10
  name: aspnetapp-ingress
spec:
  ingressClassName: webapprouting.kubernetes.azure.com
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          service:
            name: aspnetapp-service
            port:
              number: 80
        path: /
        pathType: Prefix
  tls:
  - hosts:
    - example.com
    secretName: keyvault-aspnetapp-ingress
```

# Automatically Renew SSL/TLS Certificates

Follow the instructions in the link to automatically renew certificates in Azure Key Vault before they expire using the RCL SSL AutoRenew Function app

- [RCL SSL AutoRenew Function](../autorenew/autorenew.md)
