## DHCP (Dynamic Host Configuration Protocol)

## **Overview of DHCP**  
**DHCP** is a network management protocol used to automatically assign **IP addresses** and other configuration parameters to devices on a network, enabling them to communicate. Instead of manually assigning IP addresses to each device, DHCP dynamically handles this process.

---

## **How DHCP Works – The 4-Phase Process**  
1. **Discover:**  
   - A device (client) connects to the network and sends a **DHCP Discover** message to find available DHCP servers.
   - The message is broadcasted since the client doesn’t yet have an IP address.

2. **Offer:**  
   - The DHCP server responds with a **DHCP Offer** message containing an available IP address and other network settings (e.g., subnet mask, default gateway).

3. **Request:**  
   - The client responds with a **DHCP Request** message, requesting the offered IP address.

4. **Acknowledge:**  
   - The DHCP server sends a **DHCP Acknowledgment (ACK)** to confirm the lease of the IP address.

---

## **Key Configuration Parameters Provided by DHCP**  
- **IP Address**: The unique address assigned to the device.
- **Subnet Mask**: Defines the network portion of the IP.
- **Default Gateway**: The router’s IP for external communication.
- **DNS Server**: Resolves domain names (e.g., google.com to IP addresses).

---

### **Example of a DHCP Communication**

| Step    | Message Type         | Details                                           |
|---------|----------------------|---------------------------------------------------|
| 1.      | DHCP Discover        | Client broadcasts to locate a DHCP server.        |
| 2.      | DHCP Offer           | Server offers an IP address (e.g., 192.168.1.10). |
| 3.      | DHCP Request         | Client requests the offered IP address.           |
| 4.      | DHCP Acknowledge     | Server confirms the lease of the IP address.      |

---

## **How DHCP Works – Step-by-Step**

1. **Discover:**  
- When a device (client) connects to a network, it sends a **DHCP Discover** message to find available DHCP servers.
- This message is broadcasted since the client doesn’t yet have an IP address.

2. **Offer:**  
- The DHCP server responds with a **DHCP Offer**, offering an IP address along with other settings.
- The server may offer multiple IP addresses, and the client selects one.
- The client can receive offers from multiple servers but typically accepts the first one.

3. **Request:**  
- The client responds with a **DHCP Request**, accepting the IP address offered by the server.
- This step ensures that multiple clients don’t accept the same IP address.
- The client can also request specific settings like DNS servers.

4. **Acknowledge:**  
- The server sends a **DHCP Acknowledgment (ACK)**, confirming the lease of the IP address to the client.
- The client can now use the assigned IP address and other network settings.

### **Example of a DHCP Communication Process**
| Step          | Action                    | Message Type          | Purpose                                                                 |
|---------------|---------------------------|-----------------------|-------------------------------------------------------------------------|
| 1. Discover   | Client to DHCP Server     | DHCP Discover         | “I need an IP address!”                                                 |
| 2. Offer      | DHCP Server to Client     | DHCP Offer            | “Here’s an available IP: 192.168.1.10”                                  |
| 3. Request    | Client to DHCP Server     | DHCP Request          | “I’ll take the offered IP: 192.168.1.10”                                |
| 4. Acknowledge| DHCP Server to Client     | DHCP ACK              | “IP 192.168.1.10 is yours!”                                             |


---

## **Key Components of DHCP**

1. **DHCP Server:**  
   Manages the pool of IP addresses and assigns them to clients (devices).
   - Example: A router at home acts as a DHCP server.

2. **DHCP Client:**  
   Any device (e.g., laptop, smartphone) requesting an IP address from the server.

3. **DHCP Lease:**  
   IP addresses are not assigned permanently but are leased for a specific period.  
   - Example: Lease time of **24 hours**.

4. **DHCP Relay Agent:**  
   Forwards DHCP requests between clients and servers on **different networks**.

---

## **DHCP Configuration Options Provided to Clients**

1. **IP Address**: The unique address assigned to the device.
2. **Subnet Mask**: Defines the network’s size.
3. **Default Gateway**: The router’s IP for external communication.
4. **DNS Server**: Resolves domain names into IP addresses.
5. **Lease Time**: Duration for which the IP is assigned.

---

## **Real-World Example of DHCP**  
1. **Home Network:**  
   When you connect your smartphone to Wi-Fi, the router (DHCP server) assigns it an IP address dynamically.

2. **Enterprise Network:**  
   A large office network with hundreds of devices uses DHCP to assign IP addresses automatically, avoiding conflicts and reducing the administrative workload.

---

## **Types of DHCP Allocation Methods**

1. **Dynamic Allocation:**  
   The DHCP server assigns an available IP address for a limited time (lease).  
   Example: A laptop gets IP **192.168.1.50** for 24 hours.

2. **Static Allocation (DHCP Reservation):**  
   A specific IP is reserved for a particular device based on its **MAC address**.  
   Example: A printer always receives the IP **192.168.1.100**.

3. **Automatic Allocation:**  
   The server permanently assigns an IP address that was previously used by the device.

---

## **Additional DHCP Concepts**

### 1. **DHCP Relay Agent**  
If a DHCP server and clients are on **different networks**, the router acts as a relay agent, forwarding DHCP requests to the correct server.

**Example of Router Config for Relay Agent:**
```bash
Router(config)# interface gig0/1
Router(config-if)# ip helper-address 192.168.2.1
```

---

### 2. **DHCP Lease Renewal Process**  
If a lease is about to expire, the client tries to renew it without changing the IP address.

1. **T1 Timer:** The client tries to renew the lease when 50% of the lease time has passed.
2. **T2 Timer:** If the server doesn’t respond, the client tries again at 87.5% of the lease time.

---

## **How to Configure a DHCP Server on a Router (Cisco Example)**

```bash
# Enter global configuration mode
Router> enable
Router# configure terminal

# Create a DHCP pool
Router(config)# ip dhcp pool MyNetwork
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8

# Exclude some IPs from the DHCP range
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10

# Verify DHCP configuration
Router# show ip dhcp binding
```

---

## **Python Code Example – Simulate a Simple DHCP Server**

```python
class DHCPServer:
    def __init__(self):
        self.available_ips = ["192.168.1.10", "192.168.1.11", "192.168.1.12"]
        self.leases = {}

    def discover(self, client_mac):
        print(f"DHCP Discover from {client_mac}")
        if self.available_ips:
            offered_ip = self.available_ips.pop(0)
            print(f"Offering IP: {offered_ip}")
            return offered_ip
        else:
            print("No IP available!")
            return None

    def request(self, client_mac, requested_ip):
        print(f"Request for IP {requested_ip} from {client_mac}")
        self.leases[client_mac] = requested_ip
        print(f"IP {requested_ip} leased to {client_mac}")

# Simulate a client-server interaction
dhcp_server = DHCPServer()
client_mac = "AA:BB:CC:DD:EE:FF"

offered_ip = dhcp_server.discover(client_mac)  # Discover phase
if offered_ip:
    dhcp_server.request(client_mac, offered_ip)  # Request phase
```

---

## **Advantages of Using DHCP**

1. **Ease of Management:** No need to manually configure IP addresses.
2. **Reduces Errors:** Avoids duplicate IP addresses.
3. **Scalable:** Supports growing networks without reconfiguration.
4. **Efficient:** Automatically reassigns unused IPs.

---

## **Common DHCP Issues and Solutions**

1. **IP Address Exhaustion:**  
   - **Problem:** All IPs in the pool are assigned.  
   - **Solution:** Increase the pool size or segment the network using VLANs.

2. **Lease Renewal Failure:**  
   - **Problem:** Client can’t renew the IP lease.  
   - **Solution:** Check network connectivity and DHCP server settings.

3. **DHCP Server Unavailable:**  
   - **Problem:** Clients can’t get IP addresses.  
   - **Solution:** Use a secondary DHCP server for redundancy.

---

## More Examples:

### **Example 1: DHCP Lease Time Simulation**

This example extends the basic server by introducing a **lease time** for IP addresses.


```python
import time

class DHCPServer:
    def __init__(self):
        self.available_ips = ["192.168.1.100", "192.168.1.101", "192.168.1.102"]
        self.leases = {}  # Stores leases with expiration times
        self.lease_time = 10  # Lease duration in seconds

    def offer_ip(self, client_mac):
        if client_mac in self.leases:
            ip, expiry = self.leases[client_mac]
            if time.time() < expiry:
                print(f"IP {ip} still valid for {client_mac}")
                return ip
            else:
                print(f"Lease expired for {client_mac}. Releasing IP {ip}.")
                del self.leases[client_mac]
                self.available_ips.append(ip)

        if self.available_ips:
            new_ip = self.available_ips.pop(0)
            self.leases[client_mac] = (new_ip, time.time() + self.lease_time)
            print(f"Offering IP {new_ip} to {client_mac}")
            return new_ip
        else:
            print("No IPs available!")
            return None

# Simulate DHCP interactions
server = DHCPServer()
mac = "AA:BB:CC:DD:EE:FF"

ip = server.offer_ip(mac)  # Discover and Offer
time.sleep(5)  # Simulate some time passing
server.offer_ip(mac)  # Renew lease before expiration

time.sleep(6)  # Wait until lease expires
server.offer_ip(mac)  # New IP assigned after lease expiry
```

### **Explanation:**
- **Lease Time:** Each assigned IP is valid for a limited period (10 seconds).
- **Lease Renewal:** If the lease is still valid, the same IP is provided.
- **Expiration:** Once the lease expires, the IP is released back into the pool.

---

### **Example 2: Handling Multiple Clients Simultaneously**

This example uses Python’s **`threading`** library to handle multiple clients simultaneously.


```python
import threading
import time

class DHCPServer:
    def __init__(self):
        self.available_ips = ["192.168.1.10", "192.168.1.11", "192.168.1.12"]
        self.leases = {}
        self.lock = threading.Lock()  # To handle concurrent access

    def handle_client(self, client_mac):
        with self.lock:
            if client_mac in self.leases:
                ip = self.leases[client_mac]
                print(f"Client {client_mac} already has IP: {ip}")
            else:
                if self.available_ips:
                    ip = self.available_ips.pop(0)
                    self.leases[client_mac] = ip
                    print(f"Assigned IP {ip} to {client_mac}")
                else:
                    print("No IPs available!")

    def simulate_clients(self, clients):
        threads = []
        for mac in clients:
            t = threading.Thread(target=self.handle_client, args=(mac,))
            threads.append(t)
            t.start()

        for t in threads:
            t.join()

# Simulate multiple clients connecting
server = DHCPServer()
clients = ["AA:BB:CC:DD:EE:FF", "11:22:33:44:55:66", "77:88:99:AA:BB:CC"]
server.simulate_clients(clients)
```

### **Explanation:**
- **Threading:** This example uses threads to handle multiple clients at once.
- **Concurrency Handling:** The **`lock`** ensures that multiple threads don’t modify the IP pool simultaneously, preventing race conditions.

---

### **Example 3: DHCP Server with Static Reservations**

This example introduces **reservations**, where specific MAC addresses always receive the same IP.


```python
class DHCPServer:
    def __init__(self):
        self.reservations = {"AA:BB:CC:DD:EE:FF": "192.168.1.50"}
        self.available_ips = ["192.168.1.10", "192.168.1.11"]
        self.leases = {}

    def offer_ip(self, client_mac):
        if client_mac in self.reservations:
            ip = self.reservations[client_mac]
            print(f"Reserved IP {ip} for {client_mac}")
        elif self.available_ips:
            ip = self.available_ips.pop(0)
            self.leases[client_mac] = ip
            print(f"Assigned IP {ip} to {client_mac}")
        else:
            print("No IPs available!")

# Simulate IP assignment
server = DHCPServer()
server.offer_ip("AA:BB:CC:DD:EE:FF")  # Reserved IP
server.offer_ip("11:22:33:44:55:66")  # Dynamic IP
```

### **Explanation:**
- **Reservations:** The MAC **`AA:BB:CC:DD:EE:FF`** always receives the reserved IP **192.168.1.50**.
- **Dynamic Allocation:** Other devices receive IPs from the dynamic pool.