## Application Delivery Controller (ADC)

 ### Overview

I came across the term "Application Delivery Controller" (ADC) when I searched for a component that could service as a WAF in front of your container cluster. You can think of an ADC as the evolution of a traditional load balancer. It not only distributes traffic but also provides advanced features to optimize application performance, security, and availability. ADCs are designed to handle the complexities of modern applications, especially those running in containerized environments like AKS.

## Key Features
- **Reverse Proxy**: Acts as an intermediary for requests from clients seeking resources from servers, providing an additional layer of abstraction and control.
- **Load Balancing/Routing (L4/L7)**: Distribute traffic across multiple pods and services. Supports intelligent routing (path-based, header-based).
- **Web Application Firewall (WAF)**: Protect applications from OWASP top 10 threats and filters malicious requests.
- **SSL/TLS Termination**: Https encryption at the edge
- **Health Monitoring**: Monitor application health and failover
- **Rate Limiting**: Control traffic flow and prevent overload
- **Global Traffic Management**: Geo-Routing.

## Common Solutions
- SKUDONET. Full ADC with WAF, SSL offloading, global traffic management. Acts as public entry point. Expensive, but best open-source alternative to Azure App Gatewway.
  - Runs on VM or Kubernetes deployment.
- NGINX+ModSecurity. Open-source ADC with WAF capabilities. OWASP Core Rule Set support. Can be deployed in AKS. Most flexible.
  - Runs on VM, AKS or Azure Container Instance.
- HAProxy + ModSecurity. Another open-source ADC with WAF capabilities. Best performance. Extremely fast and stable.

## Evaluation

Looking at the different products, it's hard to distinguish among pure ingress controllers, application delivery controllers and service meshes. I think most products offer a combination of feautures across those different responsibilities.

