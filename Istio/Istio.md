## Istio

Istio is een service mesh die zich richt op netwerk verkeer: 
- mTLS
- Service Discovery via Kubernetes DNS of externe DNS
- Traffic routing (canary, A/B, blue/green)
- Load balancing
- Fault injection
- Netwerklaag (L7), L7 policies
- Observability, Distributed tracing en metrics via Envoy

Kies Istio wanneer je een enterprise-grade Kubernetes cluster wilt:
- Je geavanceerde traffic control nodig hebt (canary, A/B)
- Je zero-trust networking wilt afdwingen
- Je observability op de netwerklaag nodig hebt (service-to-service metrics)

Je cluster werkt prima zonder Istio, maar je mist krachtige mesh features.
- Geen automatische mTLS versleuteling
- Je valt terug op Kubernetes network policies
- Geen identity-based security (SPIFFE/SPIRE)
- Geen canary, A/B of traffic split op version
- Alleen Kubernetes metrics (CPU, RAM)
- Geen inzicht in errors, retries, time-outs
- Geen automatische tracing (Jaeger, Tempo)
- Errors, retries, circuit breakers moet je zelf inbouwen

Istio vervangt ClusterIP niet, maar bouwt daar bovenop.

Cluster IP geeft:
- Virtueel IP binnen cluster
- Load balancing via kube-proxy
- Werkt op L4

Voorbeeld:
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP
  selector:
    app: my-app
  ports:
  - port: 80

This creates:
- A single stable IP, e.g. 10.96.12.5
- A DNS name: my-service.default.svc.cluster.local
- Load balancing to all Pods with label app=my-app

Je wilt een service, want:
- Pods are not permanent
- Pods scale up/down
- Pods restart
- Pods move between nodes
- Kubernetes networking is built around services, not pods

If you need a stable IP per pod, gebruik dan:
- StatefulSets
- Headless services 

Istio voegt daaraan toe:
- L7 routing
- mTLS versleuteling
- Traffic splitting (canary, A/B, blue/green)
- Retries, time-outs, circuit breaker

Dus: ClusterIP is alleen een eenvoudige IP router. Istio is een volledige verkeerscontroller + security laag.