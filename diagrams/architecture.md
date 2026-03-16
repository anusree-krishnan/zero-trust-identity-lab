# Zero Trust Architecture Diagram

The diagram below illustrates the trust boundary used in this lab.

```mermaid
flowchart LR

User["Kali Analyst Machine"]

subgraph Identity_Layer
SSO["GitHub SSO Login"]
end

subgraph Zero_Trust_Network
TS["Tailscale Identity Network"]
end

subgraph Protected_Server
Server["Ubuntu Server"]
Service["Web Service Port 8080"]
Sensitive["Sensitive File etc_shadow"]
end

User --> SSO
SSO --> TS
TS --> Server
Server --> Service
Service -.restricted access.-> Sensitive
