🧱 Wat zijn “Haven standaard containers” precies?
In Haven betekent een standaard container:
Een Kubernetes‑container (deployment) die voldoet aan de Haven‑specificatie, zodat deze:
- overal hetzelfde draait (cloud, on‑prem, elke leverancier)
- herbruikbaar is tussen gemeenten en andere overheden
- voorspelbaar te beheren is
- voldoet aan security‑ en compliance‑checks
- geen afhankelijkheid heeft van specifieke cloud‑features (vendor lock‑in)

📦 Wat schrijft Haven voor aan containers?
Haven definieert o.a. eisen aan:

1. Kubernetes‑objecten
Containers moeten draaien binnen een set van verplichte Kubernetes‑resources, zoals:
- Deployments
- Services
- Ingress
- ConfigMaps / Secrets
- StorageClasses (met cloud‑agnostische implementatie)

2. Security‑checks
Containers moeten voldoen aan o.a.:
- geen root‑user
- correcte network policies
- logging & metrics aanwezig
- actuele Kubernetes‑versies
- veilige opslag via StorageClasses (mag Azure/AWS‑drivers gebruiken, maar blijft Haven‑compliant) 

3. Observability
Elke container moet:
- metrics publiceren
- logs via standaard Kubernetes‑mechanismen beschikbaar maken
- health checks (liveness/readiness) hebben

4. Configuratie‑standaardisatie
Containers moeten:
- configuratie via environment variables of ConfigMaps gebruiken
- geen infrastructuurspecifieke code bevatten
- portable zijn tussen clusters

🧩 Hoe ziet een Haven‑container eruit in de praktijk?

Een typische Haven‑compliant container bevat:
- Docker image → generiek, geen cloud‑specifieke dependencies
- Deployment.yaml → met resource limits, probes, labels
- Service.yaml → standaard cluster‑IP service
- Ingress.yaml → uniforme ingress‑config
- NetworkPolicy.yaml → minimaal verkeer toegestaan
- ConfigMap/Secret → configuratie gescheiden van code
StorageClass → generiek, maar mag cloud‑driver gebruiken (Azure/AWS/S3) zolang het Kubernetes‑conform is

🧭 Waarom zijn Haven‑standaardcontainers belangrijk?
- Hergebruik tussen gemeenten
- Eenduidige aanbestedingen (“Haven‑compliant applicatie”)
- Minder vendor lock‑in
- Lagere beheerlast
- Betere security‑baseline  

