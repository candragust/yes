```mermaid
sequenceDiagram
  participant C as Client (10.0.0.10:54321)
  participant S as Server (10.0.0.80:80)

  %% TCP handshake
  C->>S: SYN
  S->>C: SYN/ACK
  C->>S: ACK
  Note over C,S: TCP 3-way handshake established

  %% HTTP request
  C->>S: POST /login HTTP/1.1
  Note right of C: Host: demo.local;
  Note right of C: User-Agent: LabBrowser/1.0;
  Note right of C: Content-Type: application/x-www-form-urlencoded;
  Note right of C: Content-Length: 30;
  Note right of C: Connection: keep-alive;
  Note right of C: Body: username=alice&amp;password=lab123

  %% HTTP response
  S-->>C: HTTP/1.1 200 OK
  Note left of S: Content-Type: text/html; charset=UTF-8
  Note left of S: Set-Cookie: sessionid=ABC123XYZ; HttpOnly
  Note left of S: Content-Length: 39
  Note left of S: Body: "Welcome alice"

  %% Persistence
  Note over C,S: HTTP/1.1 persistent connection (keep-alive)
```
