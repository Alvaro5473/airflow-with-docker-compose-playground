# Apache Airflow Playground

## Estructura de directorios

```
.
├── README.md
├── docker-compose.yaml
├── .env
├── dags/
│   └── population_pipeline.py
└── outputs/
    └── .gitignore
```

## Requisitos previos
- Docker
- Docker Compose
- Git

## Puesta en marcha

1. Iniciar los servicios:
```bash
docker-compose up -d
```

![Captura desde 2024-11-06 09-26-03](https://github.com/user-attachments/assets/243618ea-2b0e-4e7b-91d7-5c39cbcb5bf6)

2. Ver los logs (incluye la contraseña de admin):
```bash
docker-compose logs airflow | grep admin
```

![Captura desde 2024-11-06 09-30-40](https://github.com/user-attachments/assets/46510438-9646-41ac-9787-32ea507ce404)

3. Acceder a la interfaz web:
- URL: http://localhost:8001
- Usuario: admin
- Contraseña: buscar en los logs la línea que contiene "admin:password"

![Captura desde 2024-11-06 09-31-38](https://github.com/user-attachments/assets/539191dd-f64c-423d-9866-3ec5e14d2509)

![Captura desde 2024-11-06 09-32-11](https://github.com/user-attachments/assets/42319990-bfae-4499-8f6e-a7d9589baeb9)

## Verificar resultados

1. Ver el resultado en outputs:
```bash
cat outputs/report.txt
```

![Captura desde 2024-11-06 09-49-26](https://github.com/user-attachments/assets/20440fc0-dd45-4ac6-b8af-1f18f5c4c423)

2. O acceder directamente al contenedor:
```bash
docker-compose exec airflow bash
cat /tmp/report.txt
```

## Detener los servicios

```bash
docker-compose down
```

![Captura desde 2024-11-06 09-50-05](https://github.com/user-attachments/assets/ee73d0ec-7d2b-4e6f-b087-574beb4f35fb)

## Comandos útiles

- Ver logs en tiempo real:
```bash
docker-compose logs -f
```

- Reiniciar servicios:
```bash
docker-compose restart
```

- Limpiar todo (incluyendo volúmenes):
```bash
docker-compose down -v
```

## Resolución de problemas comunes

1. Si no aparece la contraseña:
   - Esperar un poco :)
   - Filtrar la salida con `docker-compose logs airflow | grep admin`

2. Si el puerto 8081 está ocupado:
   - Modificar el puerto en docker-compose.yaml: "XXXX:8080"

3. Si no aparece el DAG en la interfaz:
   - Verificar la sintaxis del archivo Python
   - Revisar los logs: `docker-compose logs airflow`

4. Si no se pueden escribir los outputs:
   - Verificar permisos en el directorio outputs
   - Comprobar la configuración de volúmenes en docker-compose.yaml
   - Regenerar el fichero de usuario: `echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env` en el raíz del proyecto.

