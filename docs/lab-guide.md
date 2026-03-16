# Zero Trust Identity Lab Guide

This guide walks through building a Zero Trust Architecture using Tailscale and Linux security controls.

## Lab Overview

This lab demonstrates how organisations move from traditional perimeter security to identity-based Zero Trust networking.

### Lab Milestones

1. Identity-Centric Connectivity
2. Micro-Segmentation
3. Principle of Least Privilege
4. Generative AI Security Analysis

## Step 1: Identity-Centric Connectivity

In traditional networks, access is granted based on IP addresses. 
In a Zero Trust Architecture, access decisions are based on identity and policy enforcement.

To create an identity-based network, we use Tailscale.

### Install Tailscale

Run the following command on both Ubuntu and Kali machines:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

Then authenticate using GitHub SSO:

```bash
sudo tailscale up
```

Verify the connection:

```bash
tailscale status
```

Both machines should now appear in the Tailscale network.
## Step 2: Creating a Protected Service

To demonstrate micro-segmentation, we first create a simple web service on the Ubuntu server.

Run the following command on the Ubuntu machine:

```bash
python3 -m http.server 8080
```

This starts a temporary web server on port 8080.

### Testing the Service

From the Kali machine, test access using:

```bash
curl http://<ubuntu-tailscale-ip>:8080
```

If successful, the web server should return a directory listing.

This confirms that the service is reachable through the Tailscale network.
## Step 3: Micro-Segmentation Using Tailscale ACLs

Micro-segmentation limits network access to only the services that are explicitly required.

In this lab, we restrict access so that users can only reach the web service running on port 8080.

### Tailscale ACL Policy

The following policy allows network members to access only port 8080.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["autogroup:members"],
      "dst": ["*:8080"]
    }
  ]
}
```

This rule allows connections only to port 8080 while blocking other services such as SSH.

### Testing the Policy

Allowed request:

```bash
curl http://<ubuntu-ip>:8080
```

Blocked request:

```bash
ssh <ubuntu-ip>
```

The SSH request should fail, demonstrating that lateral movement is restricted.
