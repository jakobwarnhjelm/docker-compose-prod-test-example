

## Scope
Recipe to manually launch two instances of the same docker compose configuration on the same Linux server.
Suitable for e.g. manual QA-testing.

The demo application is a Node.js hello-world example, behind an nginx-revsere proxy, each in a separate Docker container.



<b>compose.yaml</b> is dynamic, and prod/test is controlled through .env-file.

Copy-paste for the nginx reverse proxy config:
-  ./nginx/nginx.prod.conf
- ./nginx/nginx.test.conf

The nginx.ENV.conf file is mounted runtime from the local filesystem to the nginx container.

 The copy-pasted files could be eliminated with nginx templates
 https://stackoverflow.com/a/62844707
but might increase overall complexity unecessarily.

Launching will create two docker compose groups named after the folders the repo is cloned into. The environment variables will ensure that the container names are unique. nginx.ENV.conf contains a hardcoded reference to the value of `ENV_TYPE`

## Launch procedure prod

Create folder, clone git repo inside folder and fix `.env` file:

    cd ./prod
    git clone git@....

Change `.env` so it matches prod-settings:

    NGINX_EXPOSED_PORT=8181
    ENV_TYPE=prod

Launch with 

    docker compose up -d

## Launch procedure test
Same as for prod but change prod --> test :

    cd ./prod
    git clone git@....

Change `.env` so it matches test-settings:

    NGINX_EXPOSED_PORT=8282
    ENV_TYPE=test

Launch with 

    docker compose up -d