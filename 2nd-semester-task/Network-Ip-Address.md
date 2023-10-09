## [Exercise]() 9

### Task:

  `193.16.20.35/29`

* What is the Network IP,
* Number of hosts,
* Range of IP addresses
* and broadcast IP from this subnet?

### Instruction: 
- [ ] Submit all your answer as a markdown file in the folder for this exercise.
---
## [Solution]() 9

**Network IP (also known as Network Address):**
 - In order to determine the network IP, it is crucial to take the subnet mask into consideration. If the subnet mask is /29, the first 29 bits of the IP address are utilized for the network portion, and the remaining 3 bits are reserved for hosts. 
   - The subnet mask for /29 can be represented as 255.255.255.248 in dotted-decimal notation and 11111000 in binary. Therefore, the last 3 bits can be used for host addresses. 
   - To obtain the network address, one must zero out the host bits (the last 3 bits) and keep the network bits (the first 29 bits). It is important to note that, in this scenario, the network address is unequivocally `193.16.20.32`.
     
**Number of Hosts:**
   - It’s important to note that since this is a /29 subnet, it definitely has 3 bits available for host addresses.
   - The rules of subnetting, there's no doubt that the number of possible host addresses in a /29 subnet is 2^3 - 2 (subtracting 2 for the network address and broadcast address). 
   - So, there are 2^3 - 2 = `6 possible host addresses in this subnet`.

**Range of IP Addresses:**
   - The range of IP addresses includes all possible host addresses within the subnet.
   - In this case, the IP addresses in the range are from `193.16.20.33 to 193.16.20.38`.

**Broadcast IP (also known as Broadcast Address):**
- The broadcast address is the conclusive address in a subnet, exclusively used to send data to all hosts on the same subnet.
- To find the broadcast address, you must set all host bits to 1 while maintaining the network bits as they are.
- For the subnet 193.16.20.35/29, the broadcast address is conclusively `193.16.20.39`.

---
``` 
 Network IP (Network Address): 193.16.20.32
 Number of Hosts: 6
 Range of IP Addresses: 193.16.20.33 to 193.16.20.38
 Broadcast IP (Broadcast Address): 193.16.20.39
```


