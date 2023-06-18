## Simulación check-in de aerolínea

## Tabla de contenidos

1. [Descripción](#descripción)
2. [Desafío](#desafío)
3. [Estrategia de ramificación de Git](#estrategia-de-ramificación-de-git)
4. [Instalación local](#instalación-local)
5. [Tecnologías y lenguajes utilizados](#Tecnologías-y-lenguajes-utilizados)
6. [Documentación](#documentación)

## Descripción

Es una API REST con un solo endpoint que permita consultar por el ID del vuelo y retornar la simulación de un check-in automático de los pasajeros de la aerolínea Andes Airlines.

## Desafío

Se debe crear una API REST con un solo endpoint que permita consultar por el ID del vuelo y retornar la simulación del check-in de pasajeros. El lenguaje y/o framework es de libre elección.

Para ello se contará con una base de datos (solo lectura) que contiene todos los datos necesarios para la simulación. El servidor está configurado para que todas aquellas conexiones inactivas por más de 5 segundos sean abortadas, por lo que se requiere controlar la reconexión.

* Una compra puede tener muchas tarjetas de embarque asociadas, pero estas tarjetas pueden no tener un asiento asociado, siempre tendrá un tipo de asiento, por lo tanto, al retornar la simulación del check-in se debe asignar el asiento a cada tarjeta de embarque.

Los puntos a tomar en cuenta son:

* Todo pasajero menor de edad debe quedar al lado de al menos uno de sus acompañantes mayores de edad (se puede agrupar por el id de la compra).

* Si una compra tiene, por ejemplo, 4 tarjetas de embarque, tratar en lo posible que los asientos que se asignen estén juntos, o queden muy cercanos (ya sea en la fila o en la columna).

* Si una tarjeta de embarque pertenece a la clase “económica”, no se puede asignar un asiento de otra clase

* Los campos en la bd están llamados en Snake case, pero en la respuesta de la API deben ser transformados a Camel case.

* El servicio debe tener la siguiente estructura:

```
  GET /flights/:id/passengers
```

Respuesta exitosa:

```
{
    "code": 200,
    "data": {
        "flightId": 1,
        "takeoffDateTime": 1688207580,
        "takeoffAirport": "Aeropuerto Internacional Arturo Merino Benitez, Chile",
        "landingDateTime": 1688221980,
        "landingAirport": "Aeropuerto Internacional Jorge Cháve, Perú",
        "airplaneId": 1,
        "passengers": [
            {
                "passengerId": 98,
                "dni": 172426876,
                "name": "Abril",
                "age": 28,
                "country": "Chile",
                "boardingPassId": 496,
                "purchaseId": 3,
                "seatTypeId": 3,
                "seatId": 15
            },
            {...}
        ]
    }
}
```

Vuelo no encontrado:

```
{
"code": 404,
"data": {}
}
```

En caso de error:

```
{
"code": 400,
"errors": "could not connect to db"
}

```

## Estrategia de ramificación de Git

En este proyecto se trabaja con tres ramas:
La rama develop para agregar las funcionalides, algoritmos y configuraciones principales en la etapa de desarrollo, production para agregar las configuraciones que se requiera al hacer el despliegue de la aplicación y el main para que reuna todos los cambios de las ramas anteriores.

## Instalación local

Para ejecutar este proyecto, necesitará agregar las siguientes variables de entorno a su archivo .env

`DEBUG`

`SECRET_KEY`

`DB_NAME`

`DB_USER`

`DB_PASSWORD`

`DB_HOST`

Clonar el proyecto

```bash
$ git clone https://github.com/Geffrerson7/airline-check-in.git
```

Ir al directorio del proyecto

```bash
$ cd airline-check-in
```

Crear un entorno virtual

```sh
$ virtualenv venv
```

Activar el entorno virtual

```
# windows
$ source venv/Scripts/activate
# Linux
$ source venv/bin/activate
```

Luego instalar las librerias:

```sh
(env)$ pip install -r requirements.txt
```

Una vez concluido todo eso, procedemos a iniciar la app

```bash
(env)$ python manage.py runserver
```

Y navegar a la ruta

```sh
http://127.0.0.1:8000/
```

## Documentación
Para la documentación del proyecto se utilizó Swagger por su capacidad para generar documentación dinámica y en tiempo real de los servicios web que se están construyendo.
La documentación del projecto en swagger está en este [Link](https://airline-check-in-production.up.railway.app/swagger/)


"# Bsale" 
