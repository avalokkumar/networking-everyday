# Networking Everyday

## Introduction

Welcome to the **Networking Everyday Repository**! This repository is designed to provide a structured, day-by-day learning path for individuals interested in mastering networking concepts. Whether you're a beginner looking to build a solid foundation or someone seeking to deepen your understanding of advanced topics, this repository offers comprehensive explanations, real-world examples, and practical code snippets to facilitate your learning journey.

## Getting Started

To get started with this repository, follow these simple steps:

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/avalokkumar/networking-everyday.git
   ```

2. **Navigate to the Repository:**

   ```bash
   cd networking-everyday
   ```

3. **Explore Daily Topics:**
   
   Each day, a new folder (`Day-1`, `Day-2`, etc.) will be added with a unique networking topic. Navigate through the folders to access the content.

4. **Run Code Examples:**
   
   Inside each day’s folder, you’ll find code examples that you can run to better understand the concepts. Ensure you have the necessary programming languages and dependencies installed.

## Daily Topics

### **Day 1: IP Addressing**

- **Overview of IP Addresses:** Understanding IPv4 and IPv6.
- **Private vs. Public IPs:** Differentiating between internal and external addresses.
- **Subnetting:** Dividing networks into smaller sub-networks.
- **Real-World Example:** Setting up a home network with multiple devices.

### **Day 2: Subnetting**

- **What is Subnetting?**
- **Subnet Masks:** How to use subnet masks to create subnets.
- **CIDR Notation:** Simplifying subnet representation.
- **Practical Exercise:** Creating subnets for a small office network.

### **Day 3: VLAN (Virtual Local Area Network)**

- Introduction to VLAN
- VLAN Configuration
- VLAN Trunking
- VLAN Tagging
....

### **Day 4: DHCP (Dynamic Host Configuration Protocol)**

- Introduction to DHCP
- DHCP Lease Process
- DHCP Options
- DHCP Relay

....

### **Day 5: Networking Protocols**

- **Introduction to Protocols:** Understanding the role of protocols in networking.
- **TCP vs. UDP:** Differences and use-cases.
- **HTTP/HTTPS:** Securing web communications.
- **Example:** Setting up a simple HTTP server with Python.
  
... 

### **Day 6: NAT (Network Address Translation)**
- Introduction to NAT
- Types of NAT
- NAT Configuration
- NAT Traversal
- Example
  
... 

### **Day 7: DNS (Domain Name System)**
- Introduction to DNS
- Key Concepts of DNS
- How DNS Works – Step-by-Step Flow
- Python Example: Performing a DNS Query

... 
> *(new topics will be added later for subsequent days)*

## Examples

Example from **Day 1: IP Addressing**.

### **IP Addressing Example

```python
import socket

# Get the hostname
hostname = socket.gethostname()

# Get the IP address of the hostname
ip_address = socket.gethostbyname(hostname)

print(f"Hostname: {hostname}")
print(f"IP Address: {ip_address}")
```

**Explanation:**

This simple Python script retrieves and prints the hostname and IP address of the machine it's run on. It demonstrates how devices on a network identify themselves using IP addresses.

**Output:**

```
Hostname: my-computer
IP Address: 192.168.1.10
```

## Contributing

Contributions are welcome! If you’d like to contribute to this repository, please follow these steps:

1. **Fork the Repository:**

   Click the **Fork** button at the top right of this page.

2. **Clone Your Fork:**

   ```bash
   git clone https://github.com/avalokkumar/networking-everyday.git
   ```

3. **Create a Branch:**

   ```bash
   git checkout -b feature/new-topic
   ```

4. **Make Your Changes:**

   Add new topics, update existing content, or improve explanations and examples.

5. **Commit Your Changes:**

   ```bash
   git commit -m "Add new topic on Network Security"
   ```

6. **Push to Your Fork:**

   ```bash
   git push origin feature/new-topic
   ```

7. **Open a Pull Request:**

   Go to the original repository and click **New Pull Request**. Provide a clear description of your changes.
