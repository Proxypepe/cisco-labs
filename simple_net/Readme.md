# Laboratory work №4.Creating a network consisting of a switch and a router

## Topology

![alt text](topology.png "Topology")

## Addressing table

| Device | Interface | IP-address  | Subnet        | Default gateway | 
|--------|-----------|-------------|---------------|-----------------|
| R1     | G0/0      | 192.168.0.1 | 255.255.255.0 | -               |
| R1     | G0/1      | 192.168.1.1 | 255.255.255.0 | -               |
| PC-A   | NIC       | 192.168.1.3 | 255.255.255.0 | 192.168.1.1     |
| PC-B   | NIC       | 192.168.0.3 | 255.255.255.0 | 192.168.0.1     |

## Part 1: Device Setup and Connection Verification

### Step 1: Make static IP addressing settings on the PC interfaces.

1. Configure the IP address, subnet mask and default gateway parameters on the PC-A
   computer according to the addressing table.
2. Configure the IP address, subnet mask and parameters on the PC-B computer the default gateway
   according to the addressing table.
3. Send an echo request to PC-B from the PC-A command line.

Why did the communication check fail?

### Step 2: Configure the router.

<ol>
   <li>
      <details>
      <summary>Activate privileged EXEC mode.</summary>
      <code>
      Router> enable
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Enter global configuration mode.</summary>
      <code>
      Router# configure terminal
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Assign the router a device name according to the addressing table.</summary>
      <code>
      Router> hostname R1
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Disable DNS lookup to prevent the router from trying to convert incorrectly entered commands as if they were host names.</summary>
      <code>
      R1(config)# no ip domain-lookup 
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Assign <b>class</b> as the encrypted password of the privileged mode EXEC.</summary>
      <code>
      R1(config)# enable secret class
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Assign <b>cisco</b> as the console password and enable password login mode.</summary>
<pre>
R1(config)# line console 0
R1(config-line)# password cisco
R1(config-line)# login
</pre>
      </details>
   </li>

   <li>
      <details>
      <summary>Assign <b>cisco</b> as the password of the virtual terminal and enable password login.</summary>
<pre>
R1(config)# line vty 0 15
R1(config-line)# password cisco
R1(config-line)# login     
</pre>
      </details>
   </li>

   <li>
      <details>
      <summary>Encrypt the public passwords.</summary>
      <code>
      R1(config)# service password-encryption
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Create a banner warning about the prohibition of unauthorized access to the device.</summary>
      <code>
      R1(config)# banner motd #Unauthorized access to this device is prohibited!#
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Configure and activate both interfaces on the router.</summary>
<pre>
R1(config)# interface G0/0
R1(config-if)# ip address 192.168.0.1 255.255.255.0
R1(config-if)# no shutdown
R1(config)# interface G0/1
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
</pre>
      </details>
   </li>

  <li>
      <details>
      <summary>For each interface, enter a description indicating which device is connected to it.</summary>
<pre>
R1(config)#interface G0/0
R1(config-if)#desc
R1(config-if)#description SomeDescription
</pre>
      </details>
   </li>

   <li>
      <details>
      <summary>Save the current configuration file to the boot configuration file.</summary>
      <code>
      R1# copy running-config startup-config      
      </code>
      </details>
   </li>

  <li>
      <details>
      <summary>Set the time on the router.</summary>
      <code>
      R1# clock set 14:19:00 Oct 26 2022
      </code>
      </details>
   </li>

   <li>
      <details>
      <summary>Test the PC-B computer by sending an echo request to the PC-A computer from the command line window.</summary>
      <code>
      C:\>ping 192.168.1.3
      </code>
      </details>
   </li>
</ol>

<details>
<summary>Has the communication check been completed successfully? Why?</summary>
<code>
Yes, the request was completed successfully. The router sent an ICMP packet from one subnet to another and back.
</code>
</details>

