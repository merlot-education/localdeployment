# Local Docker deployment of the MERLOT marketplace

This repository contains relevant docker configuration for running the MERLOT marketplace stack on a local machine.

While this covers the docker part for running MERLOT locally, it is strongly advised to follow [this document](https://github.com/merlot-education/.github/blob/main/Docs/DevEnv.md) instead
to also properly set up a development WSL instance and fetch compatible microservice versions as this repository does not perform any such checks. 

Nevertheless this can be used to adjust the configuration of the docker stack when needed.

## Preparation

This compose file assumes that the orchestrator repos are cloned "next to" the localdeployment repo in order to allow for changes to the code.

### Run docker compose
Start the whole stack:
```
> docker compose up
```

Trigger a rebuild (e.g. when you change the code)
```
> docker compose up --build --force-recreate
```

If you want to debug a specific service (e.g. by running it locally on the host system), you start docker compose up with all the services listed except the specific service to debug.
For example if you wanted to leave out the contract-orchestrator, you would use 
```
> docker compose up vault postgres neo4j server keycloak rabbitmq sd-creation-wizard-api serviceoffering-orchestrator organisations-orchestrator aaam-orchestrator marketplace
```

Alternatively you can also first start the full stack and then shut down a specific service (e.g. the contract-orchestrator) with

    docker compose down contract-orchestrator