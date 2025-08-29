Instructions:

```
cd ~/Desktop/Dev/pastor
mkdir -p data
```

```
docker run -it --rm \
  -v $(pwd)/data:/data \
  -e SYNAPSE_SERVER_NAME=pastor.local \
  -e SYNAPSE_REPORT_STATS=no \
  matrixdotorg/synapse:latest generate
```

```
docker run -d \
  --name synapse \
  -v $(pwd)/data:/data \
  -p 8008:8008 \
  matrixdotorg/synapse:latest
```

```
docker run -p 8080:80 cinny:latest
```

Register an admin user ⚠

```
docker exec -it synapse register_new_matrix_user \
  -c /data/homeserver.yaml \
  -u test \
  -p testpass123 \
  -a \
  http://localhost:8008
```

Register a normal user 

```
Register an admin user ⚠

```
docker exec -it synapse register_new_matrix_user \
  -c /data/homeserver.yaml \
  -u test \
  -p testpass123 \
  http://localhost:8008
```

For Homeserver, enter: http://localhost:8008 (or http://<laptop-ip>:8008 for LAN)

Login with test / testpass123


Can create multiple users like this. You CANNOT use other servers as this is a local network only.


For it to open on pastor.local do this:

macOS/linux:
open `/etc/hosts`
do `sudo nano /etc/hosts` and then
Add:
<laptop-ip> pastor.local

Save and exit. Then flush DNS cache:
```
sudo dscacheutil -flushcache
sudo killall -HUP mDNSResponder
```
Windows:
Open Notepad as Administrator.
Open file `C:\Windows\System32\drivers\etc\hosts`
Add:
<laptop-ip> pastor.local
Save the file and exit.
Flush DNS `ipconfig /flushdns`