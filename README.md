# Firewall_Setup_task4
# Firewall Setup and Use (Windows Defender Firewall)

## I. Objective and Scope

The goal of this task was to configure and test fundamental firewall rules on a host machine. This demonstrates the critical security concept of **selective traffic filtering**—explicitly blocking insecure protocols while allowing necessary secure protocols.

**Tool Used:** Windows Defender Firewall with Advanced Security

## II. Foundational Firewall Concepts

### What is a Firewall?
A firewall is a network security system (hardware or software) that monitors and controls incoming and outgoing network traffic based on a set of predetermined security rules. It acts as a gatekeeper, isolating trusted environments (like a local computer) from untrusted networks (like the internet).

### Stateful vs. Stateless
The Windows Defender Firewall is a **stateful firewall**. This means it tracks the *state* of active connections. If a device initiates an *outbound* connection (e.g., browsing a website), the firewall automatically creates a temporary rule to allow the *inbound response traffic*, simplifying secure communication while focusing policy enforcement on *initial* inbound connections.

### Why Block Port 23 (Telnet)?
Telnet was blocked because it transmits all data, including login credentials, in **plaintext (unencrypted)**. This makes it highly vulnerable to network sniffing and eavesdropping. Blocking Port 23 enforces a more secure remote management practice.

### Why Allow Port 22 (SSH)?
SSH (Secure Shell) was chosen to be allowed because it provides an **encrypted** and secure method for remote login and management. SSH ensures data integrity and confidentiality, making it the industry standard for secure administration.

## III. Execution and Verification Steps

The following steps detail the creation, testing, and cleanup of the firewall rules. All screenshots were saved to a folder named `Screenshots/` for reference.

### Step 1: Initial Firewall Access

The Windows Defender Firewall with Advanced Security console was opened to provide a baseline for the current Inbound Rules configuration.

### Step 2: Blocking Insecure Traffic (TCP Port 23)

A new custom **Inbound Rule** was created with the action set to **Block** for **TCP Port 23** (Telnet). This rule ensures that any attempt to establish a Telnet connection to the machine is rejected at the firewall level.

### Step 3: Verifying the Block Rule

The **Telnet Client** feature was enabled. A connection attempt was made to the local machine's loopback address (`127.0.0.1`) on the blocked port (23).

**Result:** The connection failed with a timeout or "Connect failed" message, confirming that the firewall rule was active and correctly preventing the connection.

```bash
telnet 127.0.0.1 23
# Expected Output: Connecting To 127.0.0.1...Could not open connection to the host on port 23: Connect failed.
