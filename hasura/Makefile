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
	npx hasura-cli console --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}

migrate:
	npx hasura-cli migrate apply --endpoint ${HASURA_STAGING_ENDPOINT} --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}

metadata:
	npx hasura-cli metadata apply --endpoint ${HASURA_STAGING_ENDPOINT} --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}
	echo "npx hasura metadata reload and hasura migrate status too..."