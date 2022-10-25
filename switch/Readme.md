# Laboratory work №1. Building a simple network

## Topology

![alt text](topology.png "Topology")

## Addressing table

| Device | Interface | IP-address   | Subnet        |
|--------|-----------|--------------|---------------|
| PC-A   | NIC       | 192.168.0.10 | 255.255.255.0 |
| PC-B   | NIC       | 192.168.0.11 | 255.255.255.0 |
| S1     | VLAN 1    | 192.168.0.1  | 255.255.255.0 |
| S2     | VLAN 1    | 192.168.0.2  | 255.255.255.0 |

## Basic setup and verification of switch settings

### Step 1: Enter privileged EXEC mode.

<details>
<summary>What command did you use?</summary>
<code>
Switch> enable
</code>
</details>

### Step 2: Enter global configuration mode.

<details>
<summary>What command did you use?</summary>
<code>
Switch# configure terminal
</code>
</details>

### Step 3: Give the switch a name.

<details>
<summary>What command did you use?</summary>
<code>
Switch(config)# hostname some_switch
</code>
</details>

### Step 4: Prevent the switch from trying to translate bad commands as if they are node names.

<details>
<summary>What command did you use?</summary>
<code>
Switch(config)# no ip domain-lookup
</code>
</details>

<details>
<summary>What can happen if you skip this action?</summary>
By default, any single word entered on an IOS device 
that is not recognized as a valid command is treated 
as a hostname to which you want to telnet. The device
will try to translate that word to an IP address in a 
process that can last about a minute.
</details>

### Step 5: Enter local passwords.

<ol>
    <li>
        <details>
        <summary>Set a password to enter privileged mode.</summary>
        <code>Switch(config)# enable secret cisco</code>
        </details>
    </li>
    <li>
        <details>
        <summary>Set a password to access the console port and make it prompt password.</summary>
<pre>
Switch(config)# line console 0
Switch(config-line)# password cisco
Switch(config-line)# login
</pre>
        </details>
    </li>
    <li>
        <details>
        <summary>Set a password for accessing VTY lines and make it prompt for this password.</summary>
<pre>
Switch(config)# line vty 0 15
Switch(config-line)# password cisco
Switch(config-line)# login
</pre>
        </details>
    </li>
</ol>

### Step 6: Enter the MOTD banner.
<details>
<summary>Create a banner with your message</summary>
<code>
Switch(config)# no ip domain-lookup
</code>
</details>

### Step 7: Set the IP address of the SVI interface.
<details>
<summary>Set a password for accessing VTY lines and make it prompt for this password.</summary>
<pre>
Switch(config)# interface vlan1
Switch(config-if)# ip address 192.168.0.1 255.255.255.0
Switch(config-if)# no shutdown
</pre>
</details>

### Step 8: Save the configuration.
<details>
<summary>What command did you use?</summary>
<code>
Switch# copy running-config startup-config
</code>
</details>

### Step 9: Display the current configuration.
<details>
<summary>What command did you use?</summary>
<code>
Switch# show running-config
</code>
</details>

### Step 10: Display the IOS version and other switch information.
<details>
<summary>What command did you use?</summary>
<code>
Switch# show version
</code>
</details>

### Step 11: Display the status of connected switch interfaces.
<details>
<summary>What command did you use?</summary>
<code>
Switch# show ip interface brief
</code>
</details>

### Step 12: Connect to the S1 switch using the Telnet protocol.
<details>
<summary>What command did you use?</summary>
<code>
telnet 192.168.0.1
</code>
</details>
