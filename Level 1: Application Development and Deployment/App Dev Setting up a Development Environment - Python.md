# App Dev: Setting up a Development Environment - Python || [GSP183](https://www.cloudskillsboost.google/focuses/1074?parent=catalog) ||

### Run the following Commands in CloudShell

```
export ZONE=
```
```
gcloud compute instances create dev-instance --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --machine-type=e2-medium --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --metadata=enable-oslogin=true --maintenance-policy=MIGRATE --provisioning-model=STANDARD --scopes=https://www.googleapis.com/auth/cloud-platform --tags=http-server --create-disk=auto-delete=yes,boot=yes,device-name=dev-instance,image=projects/debian-cloud/global/images/debian-11-bullseye-v20240213,mode=rw,size=10,type=projects/$DEVSHELL_PROJECT_ID/zones/$ZONE/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ec-src=vm_add-gcloud --reservation-affinity=any

gcloud compute firewall-rules create allow-http --allow tcp:80 --description "Allow HTTP traffic" --direction INGRESS --target-tags http-server --network default
```
```
cat > btecky.sh <<'EOF_END'
sudo apt-get update
sudo apt-get install git -y
sudo apt-get install python3-setuptools python3-dev build-essential -y
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python3 get-pip.py
python3 --version
pip3 --version
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
ln -s ~/training-data-analyst/courses/developingapps/v1.3/python/devenv ~/devenv
cd ~/devenv/
sudo python3 server.py
EOF_END

sleep 10
```
```
gcloud compute scp btecky.sh dev-instance:/tmp --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --quiet

gcloud compute ssh dev-instance --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --quiet --command="bash /tmp/btecky.sh"
```

### Lab is completed successfully!!!

#### *Well done!*

#### Don't Forget to Join the [WhatsApp Community](https://chat.whatsapp.com/GHLPuwasldu3scnASF7JTA) & [Discussion group](https://chat.whatsapp.com/HskeXKTwaaw1duApXLAAhk)
