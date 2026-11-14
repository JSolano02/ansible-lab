# Laboratorio de Ansible con Docker
Laboratorio de Ansible con Docker


1. Iniciar los contenedores
Abrir una terminal de VS Code en la carpeta ansible-lab y ejecutar:

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





