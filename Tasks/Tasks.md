
# Remove the overly permissive rules.
Using gcloud: gcloud compute firewall-rules delete open-access
Alternatively: Go to **VPC network** > **Firewall** > Find **open-access**

# Start Bastion host
Go to **Compute Engine** > **VM Instances** > Select **bastion** > click on **Start**

# The bastion host is the one machine authorized to receive external SSH traffic. Create a firewall rule that allows SSH (tcp/22) from the IAP service. The firewall rule must be enabled for the bastion host instance using a network tag of *allow-ssh-iap-ingress-ql-332*

gcloud compute firewall-rules create <SSH IAP network tag> --allow=tcp:22 --source-ranges 35.235.240.0/20 --target-tags <SSH IAP network tag> --network acme-vpc
gcloud compute instances add-tags bastion --tags=<SSH IAP network tag> --zone=us-central1-a

# The juice-shop server serves HTTP traffic. Create a firewall rule that allows traffic on HTTP (tcp/80) to any address. The firewall rule must be enabled for the juice-shop instance using a network tag of *allow-http-ingress-ql-332*
# Create a firewall rule that allows traffic on HTTP (tcp/80) to any address and add network tag on juice-shop

gcloud compute firewall-rules create <HTTP network tag> --allow=tcp:80 --source-ranges 0.0.0.0/0 --target-tags <HTTP network tag> --network acme-vpc
gcloud compute instances add-tags juice-shop --tags=<HTTP network tag> --zone=us-central1-a

# You need to connect to juice-shop from the bastion using SSH. Create a firewall rule that allows traffic on SSH (tcp/22) from acme-mgmt-subnet network address. The firewall rule must be enabled for the juice-shop instance using a network tag of allow-ssh-internal-ingress-ql-332.
# Create a firewall rule that allows traffic on SSH (tcp/22) from acme-mgmt-subnet

gcloud compute firewall-rules create <SSH internal network tag> --allow=tcp:22 --source-ranges 192.168.10.0/24 --target-tags <SSH internal network tag> --network acme-vpc
gcloud compute instances add-tags juice-shop --tags=<SSH internal network tag> --zone=us-central1-a

# In the Compute Engine instances page, click the SSH button for the bastion host. Once connected, SSH to juice-shop.
ssh <internal IP of the juice-shop>
