ifneq (,$(wildcard ./.env))
    include .env
    export
endif

console:
	npx hasura-cli console --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}