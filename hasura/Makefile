ifneq (,$(wildcard ./.env))
    include .env
    export
endif

export REPO="${PWD}"

cmd-exists-%:
	@hash $(*) > /dev/null 2>&1 || \
		(echo "ERROR: '$(*)' must be installed and available on your PATH."; exit 1)

jwt: cmd-exists-docker
	cp -i ${REPO}/.env.example ${REPO}/.env
	sleep 1
	openssl rand -hex 32 >> ${REPO}/.env 2>&1 &

console: cmd-exists-hasura
	npx hasura-cli console --admin-secret ${HASURA_GRAPHQL_ADMIN_SECRET}