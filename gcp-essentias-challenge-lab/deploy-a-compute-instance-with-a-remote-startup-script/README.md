# Google Cloud Platform - Challenge Labs

https://google.qwiklabs.com/focuses/1735?parent=catalog

## Task 1: Create a storage bucket for startup scripts

Create a `bucket`, name it a unique name `bucket a unique globally`
```
gsutil mb -p qwiklabs-gcp-03-b229040a5600 -c STANDARD -l US -b on gs://my-bucket-20/
```
```
-p is for project ID
-c storage class
-l location
```
#### Mini Task: Upload the startup script to cloud storage bucket

Copy the `install-web.sh` and upload to your `bucket`

#### Mini Task: Make the object public available

```
gsutil acl ch -u AllUsers:R gs://my-bucket-20/install-web.sh
```

## Task 2: Create a virtual machine that runs a startup script from cloud storage

```
gcloud beta compute instances create vm-challenge --zone=us-central1-a \
--machine-type=n1-standard-1 --subnet=default --network-tier=PREMIUM \
--metadata=startup-script-url=gs://qwiklabs-gcp-03-b229040a5600/install-web.sh \
--maintenance-policy=MIGRATE \
--image=debian-9-stretch-v20200420 --image-project=debian-cloud --boot-disk-size=10GB \
--boot-disk-type=pd-standard --boot-disk-device-name=vm-challenge \
--reservation-affinity=any
```

## Task 3: Configure HTTP access for the virtual machine

```
gcloud compute firewall-rules create default-allow-http \
--direction=INGRESS \
--priority=1000 \
--network=default \
--action=ALLOW \
--rules=tcp:80 \
--source-ranges=0.0.0.0/0 \
--target-tags=http-server
```
