# Resources Used:
- https://www.python.org/doc/

# Environments Used:
- Virtual Studio Code on MacBook and Windows.

In this project, I will be building a firewall. The goal is to define a set of rules for the firewall, generate random IP numbers, then apply the rule and set the actions for the firewall.

#'Random': To generate different items.
import random

#Generate random IP address. 
def random_ip_address():
    return f"10.12.2.{random.randint(0,255)}"

#Check if any of the IP addresses matches the rule and return the corresponding action
def check_firewall_rules(ip, rules):
    for rule_ip, action in rules.items():
        if ip == rule_ip:
            return action
    return "allow"

#Set firewall rules with predefine rules where we match the IP address to block or allow with the action.
def main():
    firewall_rules = {
        "10.12.2.1": "Allow",
        "10.12.2.2": "Allow",
        "10.12.2.8": "Allow",
        "10.12.2.15": "Allow",
        "10.12.2.20": "Block",
        "10.12.2.22": "Block",
        "10.12.2.24": "Block",
        "10.12.2.50": "Allow",
        "10.12.2.70": "Allow",
        "10.12.2.85": "Block",
        "10.12.2.128": "Block",
        "10.12.2.255": "Allow",
    }

#Simulate network traffic by generating 20 random IP addresses and checking them against the firewall rules
    for _ in range(20):
        ip_address = random_ip_address()
        action = check_firewall_rules(ip_address, firewall_rules)
        random_number = random.randint(0,9999)
        print(f"IP: {ip_address}, Action: {action}, Random: {random_number}")

if __name__ == "__main__":
    main()

![image](https://github.com/user-attachments/assets/0043f450-3bd0-43b4-8f46-57333a460417)
![image](https://github.com/user-attachments/assets/f58c8649-b2df-4f5d-9e9e-bfcefc852cb2)




