# Laboratorio de Ansible con Docker

## 1. Objetivo de la práctica

El objetivo de esta práctica es aprender a utilizar Ansible para administrar y configurar varios servidores mediante Docker. Se crearon dos contenedores Ubuntu y se utilizó un Playbook para ejecutar tareas automáticamente en ambos servidores.

## 2. Tecnologías utilizadas

- Docker
- Docker Compose
- Ansible
- Ubuntu 24.04
- Python 3

## 3. Crear e iniciar los contenedores

Para iniciar los dos servidores definidos en el archivo `docker-compose.yml`, se ejecuta el siguiente comando:

```bash
docker compose up -d
```

Para comprobar que los contenedores están funcionando:

```bash
docker ps
```

## 4. Instalar Python

Se instaló Python 3 en cada contenedor utilizando los siguientes comandos:

```bash
docker exec server1 bash -c "apt-get update && apt-get install -y python3"

docker exec server2 bash -c "apt-get update && apt-get install -y python3"
```

## 5. Configurar el inventario

En el archivo `inventory.ini` se registraron los dos servidores para que Ansible pudiera administrarlos mediante la conexión Docker.

Se comprobó la conectividad utilizando:

```bash
ansible docker -i inventory.ini -m ansible.builtin.ping
```

Ambos servidores respondieron correctamente con el resultado `pong`.

## 6. Ejecutar el Playbook

Para ejecutar las tareas definidas en `playbook.yml`, se utilizó:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

El Playbook realiza las siguientes tareas:

1. Mostrar el nombre de cada servidor.
2. Mostrar el sistema operativo.
3. Crear el directorio `/tmp/ansible-demo`.
4. Crear el archivo `info.txt` con los datos del servidor.
5. Crear los directorios `logs`, `backup` y `config` mediante un loop.
6. Mostrar un mensaje cuando el sistema operativo sea Ubuntu.

## 7. Evidencia de ejecución

A continuación, se presenta la captura de pantalla de la ejecución exitosa del Playbook en ambos servidores.

**Captura de ejecución:**

![Ejecución exitosa del Playbook](captura-playbook.png)

## 8. Resultado final

La práctica se completó correctamente. Ansible logró conectarse a los dos contenedores, ejecutar las tareas definidas y crear los archivos y directorios solicitados.

Ambos servidores finalizaron la ejecución con `failed=0` y `unreachable=0`.
