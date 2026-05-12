## DAPR

- DAPR is een developer gerichte application runtime met bouwblokken voor zaken als state management, bindings naar externe systemen, pub/sub en service invocation via names (ipv IP's).
- DAPR zit op de applicatie laag (L7), niet op de netwerk laag (L4).
- Geen traffic routing, beperkte mTLS, tracing op service invocation en pub-sub (niet op netwerk verkeer).
- Dapr is geen service mesh zoals Istio. 
- DAPR draait DAPR draait als sidecar naast je applicatie.

Gebruik DAPR wanneer:
- Je microservices wilt bouwen zonder zelf state, pub/sub te implementeren.
- Je polyglot teams hebt (Go, .Net, Python, Java)
- Je applicatie logica wilt vereenvoudigen.