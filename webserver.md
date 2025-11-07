```mermaid
flowchart TD
  A[Client/Browser] --> B[DNS Resolver]
  B --> C{IP for domain?}
  C -->|Yes| D[TCP Connect to Web Server (port 80/443)]
  C -->|No/Cache| B

  D --> E[Reverse Proxy / Load Balancer (e.g., Nginx)]
  E -->|Static file| F[Serve static content]
  E -->|Dynamic request| G[App Server (e.g., Node/Flask/Django)]
  G --> H[Database / Cache / External Service]
  H --> G
  G --> E
  E --> I[HTTP Response to Client]

  %% Extras
  A -.->|TLS (if HTTPS)| D
  D -. keep-alive .- I
```
