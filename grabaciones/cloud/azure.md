---
description: Almacena tus grabaciones en un entorno propio alojado en Azure Blob
---

# Azure

{% hint style="warning" %}
Una vez ingresadas las credenciales no podrán ser vistas nuevamente, por lo que solo podrás sobrescribir.
{% endhint %}

## 1. Crear Azure Blob (opcional)

{% @arcade/embed flowId="3yGt3vDhbMVMQGy0tEot" url="https://app.arcade.software/share/3yGt3vDhbMVMQGy0tEot" %}

## 2. Crear credenciales de lectura

{% @arcade/embed flowId="PB0OiGffzg4tn4XRRmDr" url="https://app.arcade.software/share/PB0OiGffzg4tn4XRRmDr" %}

## 3. Obtener nombre del contenedor

{% @arcade/embed flowId="s2mLUPWhrU25fj9AGKL6" url="https://app.arcade.software/share/s2mLUPWhrU25fj9AGKL6" %}



## Formato de credenciales

### Opción 1

#### Connection String

Azure te da la posibilidad de proveer con una URL única de conexión que incluye todas las crendeciales necesaria para la conexión con el bucket de almacenamiento. Esta URL contiene:

* `AccountName`
* `AccountKey`
* `Protocol`
* `BlobEndpoint`

#### Ejemplo:

```
DefaultEndpointsProtocol=<protocol>;AccountName=<name>;AccountKey=<key>;BlobEndpoint=<endpoint>
```

#### Container Name

Corresponde al nombre del contenedor específico en el que se almacenarán los archivos subidos.

### Opción 2

#### Account Name

Corresponde al nombre de la cuenta Azure donde se encuentra el contenedor.

#### Account Key

Corresponde a la clave secreta que da permiso de escritura a la cuenta para el contenedor específico.

#### Protocol

Corresponde al protocolo de conexión a ser utilizado con el almacenamiento Blob de Azure, por defecto establecido como `http`, pero con posibilidad de utilizar `https`.

{% hint style="info" %}
Te sugerimos utilizar una conexión mediante `TLS`, es decir, mediante una conexión cifrada.
{% endhint %}

#### Blob Endpoint

Corresponde al endpoint facilitado por Azure en el que se almacenarán los archivos.

#### Container Name

Corresponde al nombre del contenedor específico en el que se almacenarán los archivos subidos.
