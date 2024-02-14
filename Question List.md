## Question List

1. **https 证书存放位置， https session 创建过程**

   **Certificate Storage Location (HTTPS Certificate Management):**

   HTTPS certificates, which are essential for secure communication over the web, are typically stored on web servers. These certificates are used to establish the identity of the server and encrypt data transmitted between the server and the client.

   The specific location where HTTPS certificates are stored can vary depending on the web server software being used. However, in most cases, these certificates are stored in a directory on the server's file system. The directory is often referred to as the "certificate store" or "certificate repository."

   For example, in the context of the popular web server software Apache HTTP Server, these certificates are often stored in a directory like `/etc/ssl/certs/` or `/etc/apache2/ssl/`. For Nginx, they might be stored in a directory like `/etc/nginx/ssl/`. The exact path and naming conventions can vary, so it's important to consult the documentation of your specific web server software to find the exact location.

   **HTTPS Session Creation Process:**

   The process of creating an HTTPS session involves several steps to establish a secure connection between a client (e.g., web browser) and a server. Here's a simplified overview:

   a. **Client Hello:** The client initiates the connection by sending a "Client Hello" message to the server. This message includes information about the client's capabilities and supported encryption algorithms.

   b. **Server Hello:** The server responds with a "Server Hello" message, selecting the strongest encryption algorithm that both the client and server support. It also sends its digital certificate.

   c. **Certificate Validation:** The client validates the server's certificate to ensure it's issued by a trusted Certificate Authority (CA) and hasn't expired or been revoked.

   d. **Key Exchange:** The client and server perform a key exchange using the server's public key (from the certificate) to establish a shared secret key for encryption.

   e. **Encryption:** With the shared secret key, both the client and server can encrypt and decrypt data exchanged during the session using symmetric encryption.

   f. **Secure Data Transfer:** Once the secure session is established, data can be transferred securely between the client and server.

   The details of these steps can vary based on the specific encryption protocols and algorithms used, such as TLS (Transport Layer Security), which is the modern standard for securing web communications.

   Overall, HTTPS is essential for securing data transmission over the internet, and the process involves various cryptographic techniques and certificate management to ensure confidentiality and authenticity.



2. **linux system call，至少5个**

   
   Linux system calls are functions that provide an interface between user-level programs and the kernel (the core part of the operating system). Here are at least five commonly used Linux system calls:

   1. **`open()`**: The `open()` system call is used to open files or create new ones. It returns a file descriptor that can be used for subsequent read and write operations. For example:

      ```
      cCopy code
      int fd = open("example.txt", O_RDONLY);
      ```

   2. **`read()`**: The `read()` system call is used to read data from a file or a file descriptor into a buffer. It takes the file descriptor, a buffer, and the number of bytes to read as arguments. For example:

      ```
      cCopy codechar buffer[100];
      ssize_t bytes_read = read(fd, buffer, sizeof(buffer));
      ```

   3. **`write()`**: The `write()` system call is used to write data from a buffer to a file or file descriptor. It takes the file descriptor, a buffer, and the number of bytes to write as arguments. For example:

      ```
      cCopy codechar data[] = "Hello, Linux!";
      ssize_t bytes_written = write(fd, data, sizeof(data));
      ```

   4. **`close()`**: The `close()` system call is used to close a file descriptor when it's no longer needed. It releases the associated resources. For example:

      ```
      cCopy code
      close(fd);
      ```

   5. **`fork()`**: The `fork()` system call is used to create a new process by duplicating the existing process. The new process (child) is a copy of the original (parent) and continues execution from the point of the `fork()` call. For example:

      ```
      cCopy codepid_t child_pid = fork();
      if (child_pid == 0) {
          // This code executes in the child process
      } else if (child_pid > 0) {
          // This code executes in the parent process
      } else {
          // Fork failed
      }
      ```



3. tcp flag 5个，tcp 头部

   
   TCP (Transmission Control Protocol) uses a 32-bit header to control and manage the transmission of data between two devices over a network. Within this TCP header, there are several flags (bits) that play a crucial role in controlling the behavior of the TCP connection. Here are five commonly used TCP flags:

   1. **SYN (Synchronize)**: The SYN flag is used to initiate a connection between two devices. When a device wants to establish a new TCP connection, it sends a TCP packet with the SYN flag set. The receiving device responds with a packet that has both the SYN and ACK flags set to acknowledge the connection request.
   2. **ACK (Acknowledgment)**: The ACK flag is used to acknowledge the successful receipt of data. Once a connection is established, each data packet sent between devices typically has the ACK flag set to acknowledge the receipt of the previous packet. ACKs are essential for ensuring reliable data transmission.
   3. **PSH (Push)**: The PSH flag is used to instruct the receiving device to push data to the application layer as soon as it's received, without waiting for more data to arrive. This flag is often used for interactive or real-time applications.
   4. **RST (Reset)**: The RST flag is used to reset a connection. If a device receives a packet with the RST flag set, it indicates that the sender wants to abruptly terminate the connection. This can happen if there's an error or if one party wants to forcefully close the connection.
   5. **FIN (Finish)**: The FIN flag is used to indicate the graceful termination of a connection. When a device no longer wants to send data, it sends a packet with the FIN flag set. The receiving device acknowledges the FIN, and both sides enter a closing state, allowing any remaining data to be exchanged before the connection is fully closed.

   The TCP header also includes other fields like source and destination ports, sequence and acknowledgment numbers, window size, checksum, and more, which are used to manage the connection and ensure data integrity.

   Here's a simplified representation of the TCP header:

   Source Port | Destination Port | Sequence Number| Acknowledgment Number | Data Offset | Reserved | Flags Window Size | Checksum | Urgent Pointer | Options | Data

   

4. ospf 端口号, 状态， area 类型，报文


   Certainly, here's a concise breakdown of OSPF elements:

   1. **OSPF Port Number**: OSPF (Open Shortest Path First) uses port number 89 for communication.
   2. **OSPF States**:
      - **Down**: The initial state when OSPF is not active.
      - **Init**: OSPF starts looking for neighbors and sends Hello packets.
      - **2-way**: Routers identify each other as neighbors but are not fully adjacent.
      - **ExStart**: Routers negotiate initial sequence numbers for LSAs (Link-State Advertisements).
      - **Exchange**: Routers exchange DBD (Database Description) packets containing LSA summaries.
      - **Loading**: Actual exchange of LSAs to update the link-state database.
      - **Full**: Routers synchronize their link-state databases and can forward traffic.
   3. **OSPF Area Types**:
      - **Standard Area (Area 0)**: Backbone area connecting all other areas.
      - **Stub Area**: Blocks external routes.
      - **Totally Stubby Area**: More restrictive, blocks Type 5 external LSAs.
      - **Not-So-Stubby Area (NSSA)**: Allows external routes in a controlled manner.
      - **Totally NSSA**: Similar to NSSA but with more restrictions.
   4. **OSPF Messages/Protocol Packets**:
      - **Hello**: Used for neighbor discovery and maintaining neighbor relationships.
      - **DBD (Database Description)**: Contains LSA summaries, used in the ExStart and Exchange states.
      - **LSR (Link-State Request)**: Requests specific LSAs from a neighbor.
      - **LSU (Link-State Update)**: Contains specific LSAs for updating the link-state database.
      - **LSAck (Link-State Acknowledgment)**: Acknowledges received LSUs.

   These components together enable OSPF routers to build and maintain a database of network topology, calculate shortest paths, and make routing decisions within an IP network.

   

5. ip包， 包头长度

   ![image-20230913130352910](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230913130352910.png)

   In IP (Internet Protocol), each packet (datagram) consists of a header and data payload. The header contains various fields, one of which is the "header length" field. The header length field specifies the length of the IP header in 32-bit words.

   Here's how it works:
   
   1. **Header Length Field**: This field is a 4-bit field found in the IP header. It specifies the length of the IP header in 32-bit words. Since the field is 4 bits in length, it can represent values from 0 to 15.
   2. **Calculating Header Length in Bytes**: To find the actual length of the header in bytes, you multiply the value in the header length field by 4. This is because each 32-bit word is 4 bytes long.
      - For example, if the header length field contains a value of 5, the actual header length would be 5 * 4 = 20 bytes.
   3. **Total Packet Length**: To determine the total length of the IP packet (including the header and data), you can look at another field in the IP header called the "Total Length" field. This field specifies the total length of the packet in bytes. To calculate the length of the data payload, subtract the header length (in bytes) from the total length.

   Here's a simplified representation of the IP header:
   
   ```
   mathematicaCopy code0               4               8               12              16              20              24              28
   +---------------+---------------+---------------+---------------+
   | Version   | Header Length  |    Type of Service     | Total Length            |
   +---------------+---------------+---------------+---------------+
   ```
   
   In this representation, "Header Length" is the 4-bit field we are discussing. It specifies how many 32-bit words are in the IP header. Multiply this value by 4 to get the header length in bytes, and you can then calculate the length of the data payload.



6. 以太网， 以太网帧长度

   Here's some information about Ethernet frames and frame length:

   1. **Ethernet Frame Structure**: An Ethernet frame consists of several fields, including the following key components:
      - **Preamble and Start Frame Delimiter (SFD)**: These are used for frame synchronization and to signal the start of a frame.
      - **Destination MAC Address**: Specifies the MAC (Media Access Control) address of the recipient.
      - **Source MAC Address**: Specifies the MAC address of the sender.
      - **Ethernet Type or Length**: Indicates whether the frame is using Ethernet II (Type) or IEEE 802.3 (Length) format.
      - **Data**: The actual data payload being transmitted.
      - **Frame Check Sequence (FCS)**: A checksum used for error detection.
      - **Inter-Frame Gap (IFG)**: A brief gap that separates Ethernet frames.
   2. **Ethernet Frame Length**: Ethernet frames can vary in length, and the length field in the Ethernet header specifies the length of the data portion of the frame. This field typically ranges from 46 to 1500 bytes for Ethernet II frames.
      - **Minimum Frame Length**: The minimum Ethernet frame length is 64 bytes. This includes 46 bytes of data, 18 bytes for the Ethernet header (including destination and source MAC addresses and the length/type field), and a 4-byte FCS.
      - **Maximum Frame Length**: The maximum Ethernet frame length, often referred to as the Maximum Transmission Unit (MTU), is 1518 bytes (including 4 bytes for FCS). However, in jumbo frames, the MTU can be larger, typically up to 9000 bytes or more.

   It's important to note that different Ethernet variants, such as Fast Ethernet (100 Mbps), Gigabit Ethernet (1 Gbps), and 10 Gigabit Ethernet (10 Gbps), may have different frame length specifications and maximum MTUs. Additionally, the IEEE 802.3 Ethernet standard specifies a different frame structure where the length field is used to indicate the length of the frame (including the header), while Ethernet II uses a type field to specify the type of payload.

   The specific frame length and format used in a network depend on the Ethernet variant and the network's configuration and requirements.



7. udp 头部

The User Datagram Protocol (UDP) is a simple, connectionless transport layer protocol that is part of the Internet Protocol (IP) suite. UDP provides a way to send and receive data without the reliability mechanisms found in the Transmission Control Protocol (TCP). Here's an overview of the UDP header structure:

```
diffCopy code 0      7 8     15 16    23 24    31
+--------+--------+--------+--------+
|     Source Port      | Destination Port |
+--------+--------+--------+--------+
|     Length          |    Checksum      |
+--------+--------+--------+--------+
|     Data (variable length, optional) |
+--------+--------+--------+--------+
```

The UDP header fields are as follows:

1. **Source Port (16 bits)**: This field specifies the port number of the sending application or process. It indicates the source application on the sender's side.
2. **Destination Port (16 bits)**: This field specifies the port number of the receiving application or process. It indicates the destination application on the receiver's side.
3. **Length (16 bits)**: This field specifies the length of the UDP datagram, including both the header and the data. The minimum length of a UDP header is 8 bytes, and the maximum length of a UDP datagram is 65,535 bytes.
4. **Checksum (16 bits)**: This field is used for error checking. It allows the receiver to verify the integrity of the UDP datagram. If the checksum is 0, it means that no checksum was computed for the datagram.
5. **Data**: This field is optional and can vary in length. It contains the actual data being transmitted by the UDP packet. The length of the data field is determined by the "Length" field in the header.

UDP is a lightweight protocol that does not include congestion control, flow control, or reliability mechanisms like TCP. It is often used for applications where a small amount of overhead is acceptable, and speed and minimal latency are more critical, such as real-time streaming and DNS (Domain Name System) queries. However, because UDP does not provide error recovery, it is less suitable for applications where data integrity is crucial.



8. Python dict, list 区别

Python provides both lists and dictionaries as fundamental data structures, but they serve different purposes and have distinct characteristics:

**Lists**:

1. **Ordered**: Lists are ordered collections of items, meaning the elements are stored in a specific sequence, and you can access them by their index, which starts at 0.
2. **Mutable**: Lists are mutable, which means you can modify their contents by adding, removing, or changing elements.
3. **Homogeneous**: Lists can contain elements of different data types (e.g., integers, strings, other lists, etc.).
4. **Access by Index**: You can access list elements by their position using index notation, such as `my_list[0]` to access the first element.
5. **Duplicate Elements**: Lists can contain duplicate elements, meaning the same value can appear multiple times.

**Dictionaries**:

1. **Unordered**: Dictionaries are unordered collections of key-value pairs, meaning the elements are not stored in a specific sequence, and you access them by their keys.
2. **Mutable**: Dictionaries are mutable, so you can add, remove, or modify key-value pairs.
3. **Keys Are Unique**: Dictionary keys must be unique, meaning you can't have two identical keys in the same dictionary.
4. **Keys Must Be Immutable**: Dictionary keys must be of an immutable data type (e.g., strings, numbers, or tuples). Values can be of any data type.
5. **Access by Key**: You access dictionary values by providing their associated key, like `my_dict['key']`.
6. **No Duplicates**: While keys must be unique, values in a dictionary can be duplicated.

Here's a basic comparison:

```
pythonCopy code# List example
my_list = [1, 2, 3, 4]

# Dictionary example
my_dict = {'name': 'Alice', 'age': 30, 'city': 'New York'}
```

In the list `my_list`, elements are ordered and accessed by index, while in the dictionary `my_dict`, key-value pairs are unordered and accessed by key.

You would choose between lists and dictionaries based on your specific use case. Lists are suitable for sequences of data where order matters, while dictionaries are used for mapping keys to values and retrieving values efficiently based on their keys.



9. aws service

   Amazon Web Services (AWS) is a comprehensive cloud computing platform that offers a wide range of services and solutions to help organizations with their computing, storage, networking, databases, analytics, machine learning, and more. As of my last knowledge update in September 2021, here are some of the core AWS services:

   1. **Compute Services**:

      - Amazon EC2 (Elastic Compute Cloud): Virtual machines for running applications.
      - AWS Lambda: Serverless computing for running code in response to events.
      - AWS Elastic Beanstalk: Platform as a Service (PaaS) for deploying and managing applications.

   2. **Storage Services**:

      - Amazon S3 (Simple Storage Service): Object storage for scalable data storage and retrieval.
      - Amazon EBS (Elastic Block Store): Block storage for EC2 instances.
      - Amazon Glacier: Long-term archival storage.

   3. **Database Services**:

      - Amazon RDS (Relational Database Service): Managed relational databases (e.g., MySQL, PostgreSQL, SQL Server).
      - Amazon DynamoDB: Managed NoSQL database.
      - Amazon Redshift: Data warehousing solution.

   4. **Networking Services**:

      - Amazon VPC (Virtual Private Cloud): Network isolation and connectivity options.
      - Amazon Route 53: Domain Name System (DNS) web service.
      - Elastic Load Balancing: Distributes incoming application traffic across multiple targets.

   5. **Analytics and Big Data**:

      - Amazon EMR (Elastic MapReduce): Managed Hadoop and Spark clusters.
      - Amazon Athena: Interactive query service.
      - Amazon Kinesis: Real-time data streaming and analytics.

   6. **Machine Learning and AI**:

      - Amazon SageMaker: Managed machine learning service.

      - AWS Deep Learning AMIs: Pre-configured machine learning environments.

      - AWS Lex: For building chatbots.

      - AWS Polly: Text-to-speech service

        

10. IPsec (Internet Protocol Security) is a suite of protocols used to secure network communication, providing authentication, data integrity, and confidentiality. IPsec can be configured to use various modes of negotiation, including Main Mode and Aggressive Mode, for establishing secure communication. Here's an overview of these negotiation modes and the corresponding messages:

**Main Mode**:

The following sequence of message exchange occurs during Main mode:
1. Initiator proposes the encryption and authentication algorithms to be used to establish
the VPN.
2. Responder must accept the proposal and provide the other VPN gateway with a
proposal of the encryption and authentication algorithm.
3. Initiator starts the Diffie-Hellman key exchange process by presenting a generated
public key, along with a pseudorandom number.
4. Responder responds to the initiator with its public key as part of the Diffie-Hellman
key exchange. After message 4, both parties communicate via an encrypted
channel.
5. Initiator sends the responder its IKE identity to authenticate itself.
6. Responder sends the initiator its IKE identity. Message 6 completes Phase 1 of the
IKE negotiation.

**Aggressive Mode**:

  Aggressive mode is an alternative to Main mode IPsec negotiation and it is most common
when building VPNs from client workstations to VPN gateways, where the client’s
IP address is neither known in advanced nor fixed. Aggressive mode requires half of
the messages that Main mode does when establishing Phase 1, but it does so at the cost
of disclosing the IKE identities in clear text; thus, it is a little aggressive in its security
negotiations.
Aggressive mode uses the following sequence of messages:

1. Initiator proposes the encryption and authentication algorithms to be used, begins
the Diffie-Hellman key exchange, and sends its IKE identity and pseudorandom
number.
2. Responder must accept the proposal, and will provide the initiator with a pseudorandom
number and the IKE identity of the responder. The responder will have
also authenticated the initiator in this stage.
3. Initiator authenticates the responder and confirms the exchange. At this point,
both parties have established a secure channel for negotiating the IPsec VPN in
Phase 2 and Phase 1 is now complete.

**Quick Mode**
The only mode of negotiating Phase 2 in IPsec, known as Quick mode, exchanges three
messages:
*Encryption/authentication algorithms*
The encryption and authentication algorithms which are used as part of the IPsec VPN
*Proxy IDs*
The proxy IDs which identify what traffic is part of the VPN
*Mode and encapsulation*
The VPN protocol and mode the VPN uses (ESP/AH and Tunnel/Transport) There are some additional parameters which can be configured as part of Phase 2, and they may or may not be negotiated as part of the Quick mode process.



11. BGP 状态

    GP (Border Gateway Protocol) is a complex routing protocol used in the global Internet to exchange routing and reachability information among autonomous systems (ASes). BGP routers go through several states during the BGP session establishment and maintenance process. The BGP states, also known as the BGP Finite State Machine (FSM), include:

    1. **Idle State**:
       - This is the initial state of a BGP router.
       - In this state, BGP is not operational.
       - The router waits for the BGP process to start.
    2. **Connect State**:
       - In this state, the router attempts to establish a TCP connection to the neighboring BGP router.
       - If the connection is successful, it transitions to the OpenSent state.
       - If the connection fails, it goes back to the Idle state.
    3. **OpenSent State**:
       - In this state, the router has initiated a TCP connection, and it sends an OPEN message to the neighbor.
       - It waits for an OPEN message from the neighbor in response.
       - If the OPEN message is accepted and there are no errors, it transitions to the OpenConfirm state.
       - If there is an error in the OPEN message, it transitions to the Idle state.
    4. **OpenConfirm State**:
       - In this state, the router has received an OPEN message from the neighbor and acknowledged it.
       - It now waits for a KEEPALIVE message.
       - If the KEEPALIVE message is received, it transitions to the Established state.
       - If the router receives an UPDATE message or an error, it transitions back to the Idle state.
    5. **Established State**:
       - This is the stable state of a BGP session.
       - In this state, BGP routers exchange routing updates and maintain the BGP session.
       - Routes learned from the neighbor are processed, and BGP best path selection is performed.
       - If a KEEPALIVE message is not received within the hold timer interval, the session may transition back to the OpenSent state to re-establish the connection.

    These BGP states reflect the process of establishing and maintaining BGP sessions between routers. Once a BGP session is established, routers exchange routing information and continuously update their routing tables based on BGP updates received from neighboring routers. The Established state is the desired state for normal BGP operation, as it indicates a fully functional BGP session.

12. A类地址， b类地址，C类地址, 组播地址 

    