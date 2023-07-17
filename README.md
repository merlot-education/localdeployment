### Preparation
```
> mkdir docker_data
> chmod 777 docker_data
```

### Run docker compose
```
>docker-compose up
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

### Notes
This compose is not yet complete, currently you have to start all orchestrators and the sd creation wizard api by hand for easier debugging options
