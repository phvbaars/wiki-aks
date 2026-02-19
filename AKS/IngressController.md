## Ingress Controller

There are two alternatives. When hosting your AKS cluster on the public cloud, you can only use Nginx, Traefik, HAProxy or Kong. Those ingress controllers run inside the AKS cluster. If you host AKS inside a private VNet, you can also use Azure Application Gateway Ingress Controller (AGIC). App Gateway is VNet bound.

### Functionality of ingress controller

- One public IP. 
  Without ingress, every service of type LoadBalancer gets its own public IP. Costs go up. Managing DNS becomes messy.
  With ingress, you expose one public ip. Route traffic to many services via host/path rules. Cleaner DNS.
- TLS termination in one place. 
  Without ingress, you have to manage TLS per service. 
  With ingress, you centralize certificates and certificate renewal.
- Clean routing for multiple workloads. 
  Ingress controllers give you path-based routing, host-based routing, canary releases (testing in production, small % of traffic), blue/green (blue=current, green=new, zero-downtime deployments and a safe rollback path), rate limiting and WAF (when using App Gateway Ingress Controller(=AGIc)/NGINX add-ons).

Note: ingress controllers work both with a VNet and without a VNet.

When an ingress controller doesn't add value:
- You only have one service to expose
- You don't need routing, TLS management or WAF


### API Management

De vraag is of we API Management nodig hebben naast Application Gateway. API Management  zou policies toevoegen, bijvoorbeeld voor throttling, xml->json transformatie en security (OAuth2). We kunnen APIM ook gebruiken voor het Application Gateway integratie patroon. Die functionaliteit is wel nodig voor het integratie platform, maar niet voor de container platforms. Het zou een dure oplossing zijn met weinig toegevoegde waarde.

Belangrijkste implicatie. App Gateway doet geen OAuth2 validatie voor machine-to-machine koppelingen. In dat geval kan App Gateway de authorization header alleen doorgeven (pass-through). De validatie kan dan op container niveau worden gedaan. App Gateway kan wel worden gebruikt in een user scenario. App Gateway controleert dan op de aanwezigheid van een OAuth2 token. Als dat niet geval is, vindt er een redirect plaats naar de identity provider. In een machine-to-machine scenario is dat niet mogelijk. 

Als we een andere ingress controller gebruiken dan Application Gateway, dan is gebruik van API Management helemaal vreemd. We zouden de ingress controller (in het container cluster) dan pas aanroepen na API Management. API Management staat namelijk buiten het container cluster. Dat is een onlogische architectuur.  

### FrontDoor

FrontDoor can front your AKS cluster, but it's not an ingress controller. Particularly, FrontDoor does not understand Kubernetes objects like services or pods. More in general, FrontDoor doesn't support the ingress controller functionality outlined above. FrontDoor can still be used and has added value: (1) to health probe the ingress controller, (2) multi-resgion AKS, (3) WAF at the edge.
