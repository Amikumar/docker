# knime-server

KNIME Server installation performed via
[Docker Compose](https://docs.docker.com/compose/). The installation includes:

- KNIME Server 4.12.1
- KNIME Executor 4.3.2
- RabbitMQ instance ([rabbitmq:3-management](https://hub.docker.com/_/rabbitmq))
- PostgreSQL database ([postgres:latest](https://hub.docker.com/_/postgres))
- Adminer database manager ([adminer:latest](https://hub.docker.com/_/adminer))

## Installation

### KNIME Server License

This project requires a valid KNIME Server license issued to a specific MAC
address. Follow these steps to incorporate your license into the project:

- Rename your KNIME Server license key file to `creds.xml`.
- Place your `creds.xml` file in the `container/server/license/` directory.
- Create a `.env` file in the root directory of this project.
- Add your MAC address as an environment variable to the `.env` file like so:
  - `MAC_ADDRESS=10:10:a1:a1:00:00` (update your address to match the license).

### Docker Compose

This project uses Docker Compose for a seamless installation process.
The details of the installation are configured in the `docker-compose.yaml`
file. You will need
[a valid Docker installation](https://www.docker.com/products/docker-desktop)
on your machine.

Assuming you have a valid Docker installation, run the following command from
the root folder of this project to build and deploy KNIME Server:

```bash
docker-compose build; docker-compose up -d;
```

***Note**: The `-d` flag tells Docker Compose to run in detached mode,
preventing your console from terminating the resources if you close the window.*

### Default KNIME Server configuration

The installation process utilizes the `container/server/auto-install.xml` file
to automatically configure the KNIME Server instance. Here are some of
the most pertinent default options configured in the file:

- Path to system's JDK installation: `/usr/lib/jvm/java-11-openjdk`
- Path to the installation folder: `/home/knime/knime_server`
- Workflow Repository: `/home/knime/knime_server/workflow_repository`
- Mount ID: `knime-server`
- Context Root: `knime`
- Ports:
  - HTTP: `8080`
  - HTTPS: `8443`
- Admin username: `knimeadmin`
- Admin password: `knime` (change after deploying)

### PostgreSQL database

A [PostgreSQL database](https://www.postgresql.org/) is included in this
project.

The database can be managed via an Adminer console which is available
post-installation at [http://localhost:5000/](http://localhost:5000/).
The login credentials (by default) are as follows:

- System: PostgreSQL
- Server: db
- Username: postgres
- Password: postgres
- Database: postgres

The database itself will be exposed on
[http://localhost:5432/](http://localhost:5432/). Here is an example JDBC
connection string for the default database configuration (the username and
password must also be provided).

```text
jdbc:postgresql://localhost:5432/postgres
```

You can remove the database and admin console from the `docker-compose.yaml`
file if desired.

## References

### KNIME documentation

- [KNIME Documentation](https://docs.knime.com/)
- [KNIME Server Documentation](https://docs.knime.com/?category=server&release=2020-12)
- [KNIME Server 4.12 Installation Guide](https://docs.knime.com/2020-12/server_installation_guide/index.html)

### Docker documentation

- [Docker Documentation](https://docs.docker.com/)
- [Overview of Docker Compose](https://docs.docker.com/compose/)
- [Docker Compose v3](https://docs.docker.com/compose/compose-file/compose-file-v3/)
- [The Compose Specification](https://github.com/compose-spec/compose-spec/blob/master/spec.md)

### RabbitMQ Documentation

- [RabbitMQ Documentation](https://www.rabbitmq.com/documentation.html)

### PostgreSQL documentation

- [PostgreSQL Documentation](https://www.postgresql.org/docs/current/)
- [Adminer Documentation](https://www.adminer.org/)

## Contributing

Pull requests are welcome. For major changes, please open an issue first to
discuss what you would like to change.
