# Babble 
An experimental xmpp echo bot service

## Running locally

### Prepare self signed key and certificate for STARTLS

```
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout ejabberd/localhost.key -out ejabberd/localhost.crt
openssl pkcs12 -export -clcerts -in ejabberd/localhost.crt -inkey ejabberd/localhost.key -out ejabberd/localhost.p12
openssl pkcs12 -in ejabberd/localhost.p12 -out ejabberd/localhost.pem -clcerts -nodes
```

### Run ejabberd

Start container with config that enables services at port 8888

```
docker run --name ejabberd -d -p 5222:5222 -p 8888:8888 -p 5280:5280 -v $(pwd)/ejabberd:/home/p1/cfg ejabberd/ecs
```

Optionally you can some accounts for testing

```
docker exec -it ejabberd /home/p1/ejabberd-api register --endpoint=http://127.0.0.1:5280/ --jid=admin@localhost --password=admin
docker exec -it ejabberd /home/p1/ejabberd-api register --endpoint=http://127.0.0.1:5280/ --jid=agent@localhost --password=agent
```

### Compile and run service

```
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
```
