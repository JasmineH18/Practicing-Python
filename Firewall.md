- Need to test

```
import os
from netfilterqueue import NetfilterQueue
from scapy.all import IP, TCP

# Configuration
BLACKLISTED_IPS = {"192.168.1.10", "10.0.0.50"}  # Example blocked IPs
WHITELISTED_IPS = {"192.168.1.1"}  # Example allowed IPs

def packet_filter(packet):
    payload = packet.get_payload()
    pkt = IP(payload)

    if pkt.src in WHITELISTED_IPS:
        print(f"Allowed (whitelisted): {pkt.src}")
        packet.accept()
    elif pkt.src in BLACKLISTED_IPS:
        print(f"Dropped (blacklisted): {pkt.src}")
        packet.drop()
    else:
        print(f"Accepted (default): {pkt.src}")
        packet.accept()

def setup_iptables():
    os.system("iptables -I FORWARD -j NFQUEUE --queue-num 1")
    os.system("iptables -I INPUT -j NFQUEUE --queue-num 1")

def cleanup_iptables():
    os.system("iptables -D FORWARD -j NFQUEUE --queue-num 1")
    os.system("iptables -D INPUT -j NFQUEUE --queue-num 1")

if __name__ == "__main__":
    try:
        print("[*] Starting Python firewall...")
        setup_iptables()

        nfqueue = NetfilterQueue()
        nfqueue.bind(1, packet_filter)
        nfqueue.run()
    except KeyboardInterrupt:
        print("\n[*] Stopping firewall. Cleaning up rules...")
        cleanup_iptables()
        print("[*] Done.")

    

 Ideas for Enhancements
Load whitelist/blacklist from file.

Log events to a file.

Rate-limit IPs based on connection attempts.

Add port-based rules or protocol filtering (e.g., only allow TCP port 22).

Implement a web dashboard to manage rules.

```
