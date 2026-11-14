# Laboratorio de Ansible con Docker

## Objetivo

Automatizar tareas en dos servidores Ubuntu 24.04 ejecutados como contenedores Docker. Mediante Ansible se obtiene el nombre de cada servidor y su sistema operativo, se crea `/tmp/ansible-demo` y un archivo `info.txt`, se generan los directorios `logs`, `backup` y `config` con un *loop*, y se muestra un mensaje condicionado a que el sistema sea Ubuntu.

## Archivos entregados

- `docker-compose.yml`: dos servidores Ubuntu y un servicio auxiliar con Ansible.
- `inventory.ini`: inventario con conexión directa a los contenedores Docker.
- `playbook.yml`: automatizaciones solicitadas.
- `README.md`: documentación y evidencia de ejecución.
- `captura-playbook.png`: captura **real** que se añadirá después de ejecutar correctamente el playbook.



