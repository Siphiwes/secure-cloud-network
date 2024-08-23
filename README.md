# secure-cloud-network
# scenario:
You are a security consultant brought in by Jeff, who owns a small local company, to help him with his very successful website (juiceshop). Jeff is new to Google Cloud and had his neighbour's son set up the initial site. The neighbour's son has since had to leave for college, but before leaving, he made sure the site was running.

# What's need to be done:
You need to create the appropriate security configuration for Jeff's site. Your first challenge is to set up firewall rules and virtual machine tags. You also need to ensure that SSH is only available to the bastion via IAP.
For the firewall rules, make sure that:
1. The bastion host does not have a public IP address.
2. You can only SSH to the bastion and only via IAP.
3. You can only SSH to juice-shop via the bastion.
4. Only HTTP is open to the world for juice-shop.
