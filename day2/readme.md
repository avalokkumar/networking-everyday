### What is Subnetting?

Subnetting is the practice of dividing a large network (e.g., an IP address block) into smaller, more manageable sub-networks, or "subnets." It helps improve network performance and security by reducing broadcast traffic, optimizing IP address allocation, and facilitating better control over traffic routing.


## What is a Subnet Mask?

The **Subnet Mask** determines which portion of the IP address is used for the **network** and which part is available for **hosts**.

Examples of common subnet masks:
- **255.0.0.0** = `/8` (Class A)
- **255.255.0.0** = `/16` (Class B)
- **255.255.255.0** = `/24` (Class C)

The subnet mask defines how many bits are reserved for the **network**.

## **Why Subnetting is Important?**

1. **Efficient IP Address Allocation**: Prevents wasting IP addresses.
2. **Broadcast Traffic Reduction**: Limits broadcast domains to smaller areas, improving network performance.
3. **Enhanced Security**: Subnets isolate networks, making it easier to apply security rules.

## Components of Subnetting

1. **IP Address**: Divided into two parts - the **Network ID** and the **Host ID**.
2. **Subnet Mask**: This defines which part of an IP address is the network and which part is for the hosts. It is usually represented as 255.255.255.0 or in CIDR notation like /24.
3. **CIDR Notation**: A shorthand to define subnets, e.g., `192.168.1.0/24` represents a network with a 24-bit prefix, where `192.168.1.0` is the network portion.

## How Subnetting Works:

When subnetting, the subnet mask is adjusted to split the network into smaller subnets.  
- **CIDR Notation**: Used to specify the subnet mask. E.g., `/24` means 24 bits are reserved for the network.

### **Example: Breaking Down `192.168.1.0/24`**
- **Network Address**: `192.168.1.0`  
- **Broadcast Address**: `192.168.1.255`  
- **Usable IPs**: `192.168.1.1` to `192.168.1.254` (254 usable IPs)


### Example of Subnetting

Consider an IP address `192.168.1.10` with a subnet mask `255.255.255.0`. This means:
- The first 24 bits (192.168.1) are the **Network ID**.
- The last 8 bits are the **Host ID**, which allows for 256 unique addresses (0-255) in this subnet.

#### Splitting a Larger Network
If you have a network `192.168.0.0/16`, you can split it into smaller subnets like this:
- **Subnet 1**: `192.168.1.0/24` (256 hosts)
- **Subnet 2**: `192.168.2.0/24` (256 hosts)

This allows for managing each subnet separately.

### Tools for Subnet Calculation
To make subnetting easier, you can use online subnet calculators or Python libraries to determine subnets and IP ranges.

### Python Example: Calculating Subnets

Here’s a simple example of using Python’s `ipaddress` library to calculate subnets:

```python
import ipaddress

network = ipaddress.IPv4Network('192.168.0.0/24')
subnets = list(network.subnets(new_prefix=26))  # Split into /26 subnets
for subnet in subnets:
    print(subnet)
```

Output:

```
192.168.0.0/26
192.168.0.64/26
192.168.0.128/26
192.168.0.192/26
```

This divides the original `/24` network into four smaller `/26` subnets, each allowing 64 hosts.

---

## **IP Address Structure Recap**

An IP address (IPv4) is 32 bits long and divided into **4 octets**. For example:  
**192.168.1.10**

Each octet represents 8 bits and can range from 0 to 255. This address can be represented in **binary** as:  
`11000000.10101000.00000001.00001010`

### **Division of an IP Address:**
- **Network ID**: Identifies the network the address belongs to.
- **Host ID**: Identifies the device or host within the network.

Example: In `192.168.1.10/24`, 
- **Network ID**: `192.168.1`
- **Host ID**: `10`

---

## **Subnet Calculation**

1. **CIDR Notation**: `/24` = 24 bits for network + 8 bits for host.
2. **Number of Hosts Formula**:  
   \[ \text{Hosts per subnet} = 2^{\text{Host Bits}} - 2 \]  
   Example for `/24`:
   \[ 2^8 - 2 = 254 \text{ usable hosts} \]  
   (We subtract 2 because the first address is reserved as the **network address** and the last one as the **broadcast address**.)

---

## **Subnetting Example: Creating Subnets from /24 Network**

We want to divide the **192.168.1.0/24** network into **two smaller subnets**.

1. **/24**:  
   Original range: `192.168.1.0` to `192.168.1.255` (254 hosts).

2. **/25**:  
   Splitting into two subnets:  
   - **192.168.1.0/25**: (Hosts: 0–127)  
     Usable IPs: `192.168.1.1` to `192.168.1.126`  
     Broadcast: `192.168.1.127`
   - **192.168.1.128/25**: (Hosts: 128–255)  
     Usable IPs: `192.168.1.129` to `192.168.1.254`  
     Broadcast: `192.168.1.255`

---

## **How to Calculate Subnets: Step-by-Step**

1. **Determine the Required Number of Hosts per Subnet.**
   Suppose you need **50 hosts per subnet**.

2. **Formula to Calculate Subnet Size:**
   \[ \text{Hosts} = 2^{\text{Host Bits}} - 2 \]  
   - 50 hosts → Minimum 6 host bits (since \(2^6 - 2 = 62\)).

3. **Subnet Mask for 6 Host Bits**:  
   - Network bits = 32 - 6 = 26  
   - Subnet mask: `255.255.255.192` (/26)

---

## **Subnet Calculator Example in Python**

You can use Python's `ipaddress` module to calculate subnets:

```python
import ipaddress

# Define the original network
network = ipaddress.IPv4Network('192.168.1.0/24')

# Split the network into smaller subnets with /26 mask
subnets = list(network.subnets(new_prefix=26))

# Print the subnets
for subnet in subnets:
    print(f"Subnet: {subnet} - Usable IPs: {list(subnet.hosts())}")
```

**Output:**
```
Subnet: 192.168.1.0/26 - Usable IPs: ['192.168.1.1', ..., '192.168.1.62']
Subnet: 192.168.1.64/26 - Usable IPs: ['192.168.1.65', ..., '192.168.1.126']
Subnet: 192.168.1.128/26 - Usable IPs: ['192.168.1.129', ..., '192.168.1.190']
Subnet: 192.168.1.192/26 - Usable IPs: ['192.168.1.193', ..., '192.168.1.254']
```

---

## **Advanced Topics in Subnetting**

### **1. VLSM (Variable-Length Subnet Masking)**

VLSM allows using **different subnet masks** for different parts of the network.  
Example:  
- A `/28` subnet for a small office with 14 hosts.
- A `/24` subnet for a larger office with 200 hosts.

### **2. Subnetting Class A, B, and C Networks**

- **Class A:** `10.0.0.0/8` – Very large networks.
- **Class B:** `172.16.0.0/12` – Medium-sized networks.
- **Class C:** `192.168.0.0/16` – Small networks (like home networks).

---

## **Real-World Example of Subnetting**

Imagine a university with multiple departments:
- **Science Department**: 192.168.0.0/24
- **Engineering Department**: 192.168.1.0/24
- **Library**: 192.168.2.0/24

Each department is given its own subnet, ensuring that broadcast traffic stays within the department, improving performance and security.

---

## **Summary: Subnetting at a Glance**

| **Network**         | **CIDR Notation** | **Subnet Mask**       | **Usable Hosts** |
|---------------------|-------------------|-----------------------|------------------|
| 192.168.1.0         | /24               | 255.255.255.0         | 254              |
| 192.168.1.0         | /25               | 255.255.255.128       | 126              |
| 192.168.1.0         | /26               | 255.255.255.192       | 62               |
| 192.168.1.0         | /30               | 255.255.255.252       | 2                |

---
---

## More Examples

### **1. List All IPs in a Subnet**

This example prints all the usable IP addresses within a given subnet.

```python
import ipaddress

# Define the subnet
subnet = ipaddress.IPv4Network('192.168.1.0/28', strict=False)

# List all usable IP addresses (excluding network and broadcast)
for ip in subnet.hosts():
    print(ip)
```

**Output:**
```
192.168.1.1
192.168.1.2
192.168.1.3
...
192.168.1.14
```

---

### **2. Find Network Address and Broadcast Address**

This example calculates the **network address** and **broadcast address** for a given IP range.

```python
import ipaddress

# Define the subnet
subnet = ipaddress.IPv4Network('192.168.1.0/28')

# Get network and broadcast addresses
print(f"Network Address: {subnet.network_address}")
print(f"Broadcast Address: {subnet.broadcast_address}")
```

**Output:**
```
Network Address: 192.168.1.0
Broadcast Address: 192.168.1.15
```

---

### **3. Calculate Number of Usable Hosts**

This example shows how many usable hosts exist within a given subnet.

```python
import ipaddress

# Define the subnet
subnet = ipaddress.IPv4Network('192.168.1.0/26')

# Calculate the number of usable hosts (excluding network and broadcast)
usable_hosts = len(list(subnet.hosts()))
print(f"Number of usable hosts: {usable_hosts}")
```

**Output:**
```
Number of usable hosts: 62
```

---

### **4. Split a Network into Subnets (Subnetting)**

This example demonstrates how to split a larger network into **smaller subnets**.

```python
import ipaddress

# Define the original network
network = ipaddress.IPv4Network('192.168.1.0/24')

# Split the network into smaller /26 subnets
subnets = list(network.subnets(new_prefix=26))

# Print each subnet
for subnet in subnets:
    print(subnet)
```

**Output:**
```
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

### **5. Check if an IP Belongs to a Subnet**

This example verifies whether a given IP address belongs to a specific subnet.

```python
import ipaddress

# Define the subnet and IP address
subnet = ipaddress.IPv4Network('192.168.1.0/24')
ip = ipaddress.IPv4Address('192.168.1.10')

# Check if the IP belongs to the subnet
if ip in subnet:
    print(f"{ip} belongs to {subnet}")
else:
    print(f"{ip} does not belong to {subnet}")
```

**Output:**
```
192.168.1.10 belongs to 192.168.1.0/24
```

---

### **6. Calculate the Subnet Mask for a Network**

This example retrieves the **subnet mask** of a network.

```python
import ipaddress

# Define the network
network = ipaddress.IPv4Network('192.168.1.0/24')

# Get the subnet mask
print(f"Subnet Mask: {network.netmask}")
```

**Output:**
```
Subnet Mask: 255.255.255.0
```

---

### **7. Find the First and Last Usable IPs in a Subnet**

This example retrieves the **first and last usable IP addresses** in a given subnet.

```python
import ipaddress

# Define the network
network = ipaddress.IPv4Network('192.168.1.0/28')

# Get the first and last usable IP addresses
first_ip = list(network.hosts())[0]
last_ip = list(network.hosts())[-1]

print(f"First Usable IP: {first_ip}")
print(f"Last Usable IP: {last_ip}")
```

**Output:**
```
First Usable IP: 192.168.1.1
Last Usable IP: 192.168.1.14
```

---

### **8. Convert IP Address to Binary Representation**

This example converts an IP address to its **binary form**.

```python
import ipaddress

# Define the IP address
ip = ipaddress.IPv4Address('192.168.1.10')

# Convert to binary
binary_ip = bin(int(ip))
print(f"Binary Representation: {binary_ip}")
```

**Output:**
```
Binary Representation: 0b11000000101010000000000100001010
```

---

### **9. Find Overlapping Subnets**

This example checks whether two subnets **overlap** with each other.

```python
import ipaddress

# Define two subnets
subnet1 = ipaddress.IPv4Network('192.168.1.0/25')
subnet2 = ipaddress.IPv4Network('192.168.1.64/26')

# Check if they overlap
if subnet1.overlaps(subnet2):
    print(f"{subnet1} overlaps with {subnet2}")
else:
    print(f"{subnet1} does not overlap with {subnet2}")
```

**Output:**
```
192.168.1.0/25 overlaps with 192.168.1.64/26
```

---

### **10. CIDR to Subnet Mask Conversion**

This example shows how to convert **CIDR notation** to a **subnet mask**.

```python
import ipaddress

# Define the CIDR notation
network = ipaddress.IPv4Network('192.168.1.0/26')

# Get the subnet mask
print(f"Subnet Mask: {network.netmask}")
```

**Output:**
```
Subnet Mask: 255.255.255.192
```

---

### **11. Generate All Possible Subnets of a Network**

This example splits a network into **all possible smaller subnets** with a given prefix length.

```python
import ipaddress

# Define the original network
network = ipaddress.IPv4Network('192.168.0.0/23')

# Generate smaller /25 subnets
subnets = list(network.subnets(new_prefix=25))

# Print all possible subnets
for subnet in subnets:
    print(subnet)
```

**Output:**
```
192.168.0.0/25
192.168.0.128/25
192.168.1.0/25
192.168.1.128/25
```

---

### **12. Check if an IP is Private or Public**

This example checks whether a given IP address is **private** or **public**.

```python
import ipaddress

# Define the IP address
ip = ipaddress.IPv4Address('192.168.1.10')

# Check if it is a private address
if ip.is_private:
    print(f"{ip} is a private IP address.")
else:
    print(f"{ip} is a public IP address.")
```

**Output:**
```
192.168.1.10 is a private IP address.
```
