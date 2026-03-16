
    ## Application Delivery Controller (ADC)

    ### Overview

    I came across the term "Application Delivery Controller" (ADC) when I searched for a component that could service as a WAF in front of your container cluster. You can think of an ADC as the evolution of a traditional load balancer. It not only distributes traffic but also provides advanced features to optimize application performance, security, and availability. ADCs are designed to handle the complexities of modern applications, especially those running in containerized environments like AKS.

    ## Key Features
    - **Load Balancing (L4/L7)**: Distribute traffic across multiple pods and services. Supports intelligent routing (path-based, header-based).
    - ** Web Application Firewall (WAF)**: Protect applications from OWASP top 10 threats and filters malicious requests.
    - **Health Monitoring**: Monitor application health and failover
    - **SSL/TLS Termination**: Https encryption at the edge
    - **Rate Limiting**: Control traffic flow and prevent overload
    - **Global Traffic Management**: Geo-Routing.

    ## Common Solutions
    - Ingress Controllers (NGINX, Traefik)
    - Service Mesh (Istio, Linkerd)
    - API Gateways (Kong, Apigee)

    ### AKS Integration
    ADCs on AKS provide centralized traffic management and enable advanced routing capabilities for containerized applications.
