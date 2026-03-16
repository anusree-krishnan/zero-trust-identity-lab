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
