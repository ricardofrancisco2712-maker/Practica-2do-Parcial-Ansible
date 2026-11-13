<img width="1920" height="1080" alt="Captura de pantalla 2026-11-13 134713" src="https://github.com/user-attachments/assets/477d7b7c-d2c5-4cb4-b90b-d49fc75e127e" />
<img width="1920" height="1080" alt="Captura de pantalla 2026-11-13 134626" src="https://github.com/user-attachments/assets/d7e8a983-5a40-4a89-93b1-866dcdd886ed" />
\# Laboratorio Ansible con Docker



\## Objetivo de la práctica



Crear un laboratorio con dos servidores Linux (Ubuntu 24.04) usando contenedores Docker y administrarlos con Ansible: verificar la conexión con un inventario, y ejecutar un playbook que recopila información de los servidores, crea directorios y archivos, usa `loop` y ejecuta tareas condicionales (`when`).



\## Estructura



```text

ansible-lab/

├── docker-compose.yml

├── inventory.ini

├── playbook.yml

└── README.md

```



\## Requisitos



\- Docker y Docker Compose

\- Ansible (paquete completo `ansible`, o `ansible-core` + `ansible-galaxy collection install community.docker`, necesaria para `ansible\_connection=docker`)



\## Comandos para iniciar los contenedores



```bash

docker compose up -d

docker ps

```



Instalar Python en cada contenedor (requerido por Ansible):



```bash

docker exec server1 bash -c "apt update \&\& apt install -y python3"

docker exec server2 bash -c "apt update \&\& apt install -y python3"

```



\## Comprobar la conexión



```bash

ansible docker -i inventory.ini -m ping

```



\## Comando para ejecutar el playbook



```bash

ansible-playbook -i inventory.ini playbook.yml

```



\## Qué hace el playbook



1\. Muestra el nombre del host.

2\. Muestra el sistema operativo.

3\. Crea `/tmp/ansible-demo`.

4\. Crea `info.txt` con el nombre del servidor y el sistema operativo.

5\. Crea con un `loop` los directorios `logs`, `backup` y `config`.

6\. Muestra un mensaje solo cuando el sistema operativo es Ubuntu.



\## Verificar el resultado



```bash

docker exec server1 cat /tmp/ansible-demo/info.txt

docker exec server2 ls /tmp/ansible-demo

```



\## Captura de pantalla de la ejecución exitosa



!\[Ejecución exitosa del playbook](captura-playbook.png)



\## Detener el laboratorio



```bash

docker compose down

```
<img width="1920" height="1080" alt="Captura de pantalla 2026-11-13 134626" src="https://github.com/user-attachments/assets/6912514b-fc43-441c-95ca-6d3bda164616" />

