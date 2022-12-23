# next-auth-hasura-example

> An example repo of using `next-auth` with Hasura as the back-end. Based on [https://hasura.io/learn/graphql/hasura-authentication/integrations/nextjs-auth/](https://hasura.io/learn/graphql/hasura-authentication/integrations/nextjs-auth/)

Required:
- [Node v14](https://nodejs.org/download/release/latest-v14.x/)
- [Yarn](https://classic.yarnpkg.com/en/docs/install/)
- [Git](https://git-scm.com/downloads)
- [Docker](https://docs.docker.com/get-started/overview/)
- [Hasura CLI](https://hasura.io/docs/latest/graphql/core/hasura-cli/install-hasura-cli.html)

# Setting up Hasura

### To launch Hasura for development

> For the first time:

```sh
cd hasura
make jwt
# it will copy .env.example to .env and create JWT token inside your .env
```

> Then

```sh
cd hasura
docker-compose up -d
# will launch postgres and Hasura containers
make console
# Will start Hasura console and tracking change (metadata/migrations) from the GUI.
```

### Regroup your Hasura changes

> Every action on your postgres tables will create a migration folder with timestamps and the sql code, you can merge these with the squash command.

```sh
hasura migrate squash --name 'squash-given-name' --from '{your older timestamps folder}'
```

> testing migrations

To test you newly created migrations what you can do is to reproduice a fresh install. To do so you can create a new repo and git clone this repo and copy your migrations but you will have to change the network Id and the db name inside your docker-compose.yaml, or you can delete your db without the need to create a new repo.

```sh

# Clean up Docker
cd /hasura
docker-compose down
docker volume ls
#... see the one you want to remove maybe "hasura_db_..."
docker volume rm name_of_your_volume
# now you can docker-compose up and do the migration (metadata and migrations)
```

## 🚀 Deployment

> Hasura: use the hasura cli with the `Makefile`

```sh
# for your local or staging (not prod)
make migrate
```

> track all tables and relationships

Click `Track all` both for the tables and the relationships

![image](https://user-images.githubusercontent.com/12476396/209340702-1b24018d-d597-41f5-b3d0-c203b9b5b524.png)
![image](https://user-images.githubusercontent.com/12476396/209340886-4049cd14-8f82-4d65-9af4-727f169fc7e8.png)

