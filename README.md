### Preparation
Create a folder for persisting docker data:
```
> mkdir docker_data
> chmod 777 docker_data
```
This compose file also assumes that the orchestrator repos are cloned "next to" the localdeployment repo in order to allow for changes to the code.

### Run docker compose
Start the whole stack:
```
> docker-compose up
```

Trigger a rebuild (e.g. when you change the code)
```
> docker-compose up --build
```

If you want to debug a specific service (e.g. by running it locally on the host system), you start docker compose up with all the services listed except the specific service to debug.
For example if you wanted to leave out the contract-orchestrator, you would use 
```
> docker-compose up vault postgres neo4j server keycloak rabbitmq sd-creation-wizard-api serviceoffering-orchestrator organisations-orchestrator aaam-orchestrator marketplace
```

### Keycloak setup

When all components started you should setup Keycloak which is used as Identity and Access Management layer in the project. Add keycloak host to your local `hosts` file:

```
127.0.0.1	key-server
```

- Open keycloak admin console at `http://key-server:8080/admin`, with `admin/admin` credentials, select `gaia-x` realm. 
- Go to `Clients` section, select `federated-catalogue` client, go to Credentials tab, Regenerate client Secret, copy it and set to `/docker/.env` file in `FC_CLIENT_SECRET` variable
- Go to users and create one to work with. Set its username and other attributes, save. Then go to Credentials tab, set its password twice, disable Temporary switch, save. Go to Role Mappings tab, in Client Roles drop-down box choose `federated-catalogue` client, select `Ro-MU-CA` role and add it to Assigned Roles.
- Restart docker compose to pick up changes applied at the second step above.
