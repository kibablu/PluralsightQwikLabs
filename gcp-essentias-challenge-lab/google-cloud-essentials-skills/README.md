# Google Cloud Platform - Challenge Labs

https://google.qwiklabs.com/quests/47

## Task 1: Create a Linux Virtual Machine Instance

Create a `Linux virtual machine`, name it "apache" and specify the zone as "us-central1-a".
```
gcloud compute instances create apache \
    --zone=us-central1-a \
    --machine-type=n1-standard-1 \
    --subnet=default \
    --network-tier=PREMIUM \
    --maintenance-policy=MIGRATE \
    --tags=http-server \
    --image=ubuntu-1804-bionic-v20200414 \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=10GB \
    --boot-disk-type=pd-standard \
    --boot-disk-device-name=apache \
    --no-shielded-secure-boot \
    --shielded-vtpm \
    --shielded-integrity-monitoring \
    --reservation-affinity=any   
 ```
       
## Task 2: Enable public access to VM instance

While creating the `Linux instance`, make sure to apply the appropriate `firewall rules` so that potential customers can find your new product.
```
gcloud compute firewall-rules create \
    default-allow-http \ 
    --direction=INGRESS \
    --priority=1000 \
    --network=default \
    --action=ALLOW \
    --rules=tcp:80 \
    --source-ranges=0.0.0.0/0 \
    --target-tags=http-server
```    

## Task 3: Running basic Apache Web Server

A virtual machine instance on `Google Compute Engine` can be controlled like any standard Linux server. Deploy a simple Apache web server (a placeholder for the new product site) to learn the basics of running a server on a virtual machine instance.
```
sudo apt update
sudo apt install apache2
```

## Task 4: Test your server

Test that your instance is serving traffic on its external IP. You should see the `Apache2 Ubuntu Default page` 
```
Trying accessing the VM using an https address. \
Check that your URL is http:// EXTERNAL_IP and not https:// EXTERNAL_IP
```
