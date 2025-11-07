```mermaid
sequenceDiagram
  autonumber
  participant C as Client (10.0.0.10:54321)
  participant S as Server (10.0.0.80:80)

  Note over C,S: TCP 3-Way Handshake
  C->>S: SYN
  S->>C: SYN/ACK
  C->>S: ACK

  Note over C,S: HTTP Request (plaintext HTTP/1.1)
  C->>S: POST /login HTTP/1.1
  Note right of C:
    Host: demo.local
    User-Agent: LabBrowser/1.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 30
    Connection: keep-alive
    Body: username=alice&amp;password=lab123
  end note

  Note over C,S: HTTP Response
  S-->>C: HTTP/1.1 200 OK
  Note left of S
    Content-Type: text/html; charset=UTF-8
    Set-Cookie: sessionid=ABC123XYZ; HttpOnly
    Content-Length: 39
    Body: &lt;html&gt;&lt;body&gt;Welcome alice&lt;/body&gt;&lt;/html&gt;
  end note

  Note over C,S: HTTP/1.1 persistent connection (keep-alive)
```
