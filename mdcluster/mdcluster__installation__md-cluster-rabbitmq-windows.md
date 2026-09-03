<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-rabbitmq-windows -->

# Windows

Requires RabbitMQ version 4.2 or later.

Please refer to [the link](https://www.rabbitmq.com/docs/which-erlang#compatibility-matrix) for the Erlang-RabbitMQ compatibility matrix.

### [Prerequisites](/docs/mdcluster/installation/md-cluster-rabbitmq-windows#prerequisites)

Before installing the RabbitMQ service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Windows 11 23H2+, or Windows Server 2019+. |
| Privileges | Administrator privileges. |
| Hardware | 4 vCPU and 8 GB RAM. |
| Disk space | At least 100 GB of available storage. |
| Network access | Required ports are open:   - **5672** — AMQP client connections (default). - **15672** — Management UI (optional).   A minimum network bandwidth of **1 Gbps** is required. |

### [Install Erlang/OTP](/docs/mdcluster/installation/md-cluster-rabbitmq-windows#install-erlangotp)

1. Download [Erlang/OTP 26.2.5.18](https://github.com/erlang/otp/releases/download/OTP-26.2.5.18/otp_win64_26.2.5.18.exe).
2. Run the downloaded installer.

### [Install RabbitMQ](/docs/mdcluster/installation/md-cluster-rabbitmq-windows#install-rabbitmq)

1. Download [RabbitMQ 4.2.5](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-4.2.5.exe).
2. Run installer.
3. Pick an install directory.
4. In Command Prompt, run the command as **Administrator** to set up user.

cd <RabbitMQ_sbin_dir> # default: "C:\Program Files\RabbitMQ Server\rabbitmq_server-4.2.5\sbin"
rabbitmqctl.bat add_user <username> <password>
rabbitmqctl.bat set_permissions -p / <username> "." "." "."
rabbitmqctl.bat set_user_tags <username> administrator
