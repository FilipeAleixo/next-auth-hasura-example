ifneq (,$(wildcard ./.env))
    include .env
    export
endif

export REPO="${PWD}"

jwt:
	cp -i ${REPO}/.env.example ${REPO}/.env
	sleep 1
	openssl rand -hex 32 >> ${REPO}/.env 2>&1 &

console:
	npx hasura console --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}

migrate-apply:
	npx hasura migrate apply --endpoint ${HASURA_STAGING_ENDPOINT} --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}

metadata-apply:
	npx hasura metadata apply --endpoint ${HASURA_STAGING_ENDPOINT} --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}