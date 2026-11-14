# Laboratorio de Ansible con Docker

## Objetivo

Automatizar tareas en dos servidores Ubuntu 24.04 ejecutados como contenedores Docker. Mediante Ansible se obtiene el nombre de cada servidor y su sistema operativo, se crea `/tmp/ansible-demo` y un archivo `info.txt`, se generan los directorios `logs`, `backup` y `config` con un *loop*, y se muestra un mensaje condicionado a que el sistema sea Ubuntu. 

## Archivos entregados

- `docker-compose.yml`: dos servidores Ubuntu y un servicio auxiliar con Ansible.
- `inventory.ini`: inventario con conexión directa a los contenedores Docker.
- `playbook.yml`: automatizaciones solicitadas.
- `README.md`: documentación y evidencia de ejecución.
- `captura-playbook.png`: captura **real** que se añadirá después de ejecutar correctamente el playbook.

## Requisitos

- Docker Desktop iniciado.
- Visual Studio Code (o una terminal de PowerShell).
- No se requiere instalar Ubuntu/WSL adicional ni Ansible en Windows.

El servicio `controlador` es una herramienta auxiliar dentro de Docker. La práctica sigue usando **dos servidores**, `server1` y `server2`. Ansible se comunica por el conector `community.docker.docker` (nombre completo de la conexión Docker), sin SSH. El controlador monta el socket local de Docker; úsalo solo para este laboratorio y no con código no confiable.

## 1. Iniciar los contenedores

Abrir una terminal de VS Code en la carpeta `ansible-lab` y ejecutar:

docker compose up -d --build
docker ps

Deberían mostrarse server1, server2 y ansible-lab-controlador-1 (el nombre del servicio auxiliar puede llevar prefijos).

2. Instalar Python 3 en los dos servidores
Los contenedores Ubuntu mínimos no incluyen necesariamente Python; Ansible lo necesita para recopilar datos y ejecutar módulos.

docker exec server1 bash -c "apt-get update && apt-get install -y python3"
docker exec server2 bash -c "apt-get update && apt-get install -y python3"

Esta instalación se hace dentro de los contenedores. Si se eliminan y recrean desde cero, habrá que repetirla.

3. Verificar la conexión de Ansible
docker compose exec controlador ansible docker -i inventory.ini -m ping

Los dos servidores deben responder SUCCESS con "ping": "pong".

4. Ejecutar el playbook
docker compose exec controlador ansible-playbook -i inventory.ini playbook.yml

El resumen final PLAY RECAP debe indicar failed=0 y unreachable=0 para server1 y server2.

5. Verificar los resultados
docker exec server1 cat /tmp/ansible-demo/info.txt
docker exec server2 cat /tmp/ansible-demo/info.txt
docker exec server1 ls -l /tmp/ansible-demo
docker exec server2 ls -l /tmp/ansible-demo

Cada servidor debe contener su propio info.txt y los tres directorios logs, backup y config.

Evidencia de ejecución exitosa



<img width="1390" height="837" alt="image" src="https://github.com/user-attachments/assets/b3003c2d-2f35-43a8-8bed-0d59124a3dea" />





