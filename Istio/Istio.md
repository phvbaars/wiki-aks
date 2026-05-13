## Istio

Istio is een service mesh die zich richt op netwerk verkeer: 
- mTLS
- Service Discovery via Kubernetes DNS of externe DNS
- Traffic routing (canary, A/B, blue/green)
- Load balancing
- Fault injection
- Netwerklaag (L7), L7 policies
- Observability, Distributed tracing en metrics via Envoy

Kies Istio wanneer:
- Je geavanceerde traffic control nodig hebt (canary, A/B)
- Je zero-trust networking wilt afdwingen
- Je observability op de netwerklaag nodig hebt

Je cluster werkt prima zonder Istio, maar je mist krachtige mesh features.
- Geen automatische mTLS versleuteling
- Je valt terug op Kubernetes network policies
- Geen identity-based security (SPIFFE/SPIRE)
- Geen canary, A/B of traffic split op version
- Alleen Kubernetes metrics (CPU, RAM)
- Geen inzicht in errors, retries, time-outs
- Geen automatische tracing (Jaeger, Tempo)
- Errors, retries, circuit breakers moet je zelf inbouwen
