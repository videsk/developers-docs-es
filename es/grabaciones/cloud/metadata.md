# Metadata

Una vez que la integración para sincronizar las grabaciones esté completada y correcta, se comenzarán a enviar con metadata asociada a la llamada, lo que te permitirá buscar grabaciones de una manera enriquecida.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Por defecto, adjuntamos:

| Clave       | Valor  | Descripción                                              |
| ----------- | ------ | -------------------------------------------------------- |
| duration    | Number | Duración de la grabación en minutos                      |
| checkSum    | String | CheckSum de la grabación con SHA-1                       |
| startedAt   | Date   | Timestamp en la que comenzó la grabación                 |
| endedAt     | Date   | Timestamp en la que finalizó la grabación                |
| user        | String | ID del ejecutivo                                         |
| extension   | String | Extensión del archivo, por defecto: _webm_.              |
| uploadDate  | Date   | Fecha en la que se intentó sincronizar con cloud storage |
| recordingId | String | ID de las pistas (no llamada)                            |
| size        | Number | Tamaño del archivo en bytes                              |
| identifier  | String | ID de la llamada                                         |
| contentType | String | MIME type del archivo, por defecto: _video/webm_.        |
