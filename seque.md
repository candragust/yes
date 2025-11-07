```mermaid
sequenceDiagram
    autonumber
    participant C as Client (10.0.0.10:54321)
    participant S as Server (10.0.0.80:80)

    rect rgb(245,245,245)
    note over C,S: TCP 3-Way Handshake
    C->>S: SYN
    S->>C: SYN/ACK
    C->>S: ACK
    end

    rect rgb(235,250,255)
    note over C,S: HTTP Request (plaintext HTTP/1.1)
    C->>S: POST /login HTTP/1.1
    Note right of C: "Host: demo.local\nUser-Agent: LabBrowser/1.0\nContent-Type: application/x-www-form-urlencoded\nContent-Length: 30\nConnection: keep-alive\n\nusername=alice&password=lab123"
    end

    rect rgb(235,255,235)
    note over C,S: HTTP Response
    S-->>C: HTTP/1.1 200 OK
    Note left of S: "Content-Type: text/html; charset=UTF-8\nSet-Cookie: sessionid=ABC123XYZ; HttpOnly\nContent-Length: 39\n\n<html><body>Welcome alice</body></html>
    end"

    Note over C,S: HTTP/1.1 default persistent connection (keep-alive)
```
