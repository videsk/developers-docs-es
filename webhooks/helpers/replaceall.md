# replaceAll

Este helper reemplaza **todas** las ocurrencias de un valor dentro de un `String` por un valor de reemplazo. Soporta dos modos: reemplazo de texto plano y reemplazo por expresión regular.

{% hint style="info" %}
A diferencia del método `String.prototype.replace` nativo de JavaScript, este helper siempre reemplaza todas las coincidencias y no solo la primera.
{% endhint %}

## Modo de uso

```handlebars
{{replaceAll input search replacement [flags]}}
```

| Parámetro     | Tipo     | Requerido | Por defecto |
|---------------|----------|-----------|-------------|
| `input`       | `String` | ✓         | —           |
| `search`      | `String` | ✓         | —           |
| `replacement` | `String` | ✗         | `""`        |
| `flags`       | `String` | ✗         | —           |

Cuando se proporciona el cuarto parámetro `flags`, el helper interpreta `search` como un patrón de expresión regular. El flag `g` se añade automáticamente para garantizar el reemplazo global, aunque no lo incluyas explícitamente.

### Ejemplos

{% tabs %}
{% tab title="Reemplazo simple" %}
```handlebars
{{replaceAll customer.note "foo" "bar"}}
```

Entrada: `"foo foo foo"` → Salida: `"bar bar bar"`
{% endtab %}

{% tab title="Eliminar caracteres" %}
```handlebars
{{replaceAll customer.phone "-"}}
```

Cuando no se proporciona reemplazo, las coincidencias se eliminan.

Entrada: `"+56-9-1234-5678"` → Salida: `"+56912345678"`
{% endtab %}

{% tab title="Regex con flags" %}
```handlebars
{{replaceAll input "[0-9]+" "#" "g"}}
```

Entrada: `"a1b22c333"` → Salida: `"a#b#c#"`
{% endtab %}

{% tab title="Case-insensitive" %}
```handlebars
{{replaceAll input "hola" "chao" "i"}}
```

Entrada: `"Hola Hola HOLA"` → Salida: `"chao chao chao"`
{% endtab %}

{% tab title="Capture groups" %}
```handlebars
{{replaceAll input "(\w+)@(\w+)" "$2-$1" "g"}}
```

Entrada: `"john@videsk and jane@videsk"` → Salida: `"videsk-john and videsk-jane"`
{% endtab %}
{% endtabs %}

## Configuración

### `input`

El texto sobre el que se aplicará el reemplazo. Puede ser una referencia a una variable del contexto o un valor literal. Los valores que no sean `String` se convierten automáticamente.

{% hint style="danger" %}
Si `input` es `undefined` o `null`, el helper retornará un error: `Error: Input string is required`.
{% endhint %}

```handlebars
{{replaceAll customer.message "hola" "chao"}}
```

### `search`

El valor a buscar dentro de `input`. Su interpretación depende de si se entrega o no el parámetro `flags`:

* **Modo string plano** (sin `flags`): `search` se trata como texto literal. Los caracteres especiales de expresiones regulares (`.`, `*`, `[`, `(`, etc.) **no** son interpretados.
* **Modo regex** (con `flags`): `search` se interpreta como patrón de expresión regular estándar de JavaScript.

{% hint style="danger" %}
Si `search` es `undefined` o `null`, el helper retornará un error: `Error: Search value is required`.
{% endhint %}

{% tabs %}
{% tab title="Como texto literal" %}
```handlebars
{{replaceAll input "a.b" "X"}}
```

Entrada: `"a.b aXb a.b"` → Salida: `"X aXb X"`

El punto `.` se trata como un carácter literal, no como comodín.
{% endtab %}

{% tab title="Como regex" %}
```handlebars
{{replaceAll input "a.b" "X" "g"}}
```

Entrada: `"a.b aXb a.b"` → Salida: `"X X X"`

El punto `.` actúa como comodín y coincide con cualquier carácter.
{% endtab %}
{% endtabs %}

### `replacement`

El valor que sustituirá a cada coincidencia. Es opcional: si se omite, las coincidencias se eliminan del texto.

En modo regex, puedes referenciar los grupos de captura usando `$1`, `$2`, etc.

```handlebars
{{replaceAll input "(\d{4})-(\d{2})-(\d{2})" "$3/$2/$1" "g"}}
```

Entrada: `"2026-05-12"` → Salida: `"12/05/2026"`

### `flags`

Activan el modo regex y definen el comportamiento de la expresión regular. Acepta cualquier combinación válida de flags de JavaScript.

{% hint style="info" %}
El flag `g` (global) se agrega automáticamente si no está presente, para asegurar el reemplazo de todas las coincidencias.
{% endhint %}

| Flag | Descripción                                                                |
|------|----------------------------------------------------------------------------|
| `g`  | Global. Se aplica automáticamente, lo incluyas o no.                       |
| `i`  | Case-insensitive: no distingue mayúsculas y minúsculas.                    |
| `m`  | Multilínea: `^` y `$` coinciden al inicio y fin de cada línea.             |
| `s`  | Permite que `.` coincida también con saltos de línea.                      |
| `u`  | Trata el patrón como Unicode.                                              |

## Errores comunes

| Error                                     | Causa                                                                                            |
|-------------------------------------------|--------------------------------------------------------------------------------------------------|
| `Error: Input string is required`         | El parámetro `input` está vacío o no resuelve ningún valor.                                      |
| `Error: Search value is required`         | El parámetro `search` está vacío o no resuelve ningún valor.                                     |
| `Error: Invalid regex pattern: <detalle>` | El patrón regex tiene una sintaxis inválida (por ejemplo, un corchete `[` sin cerrar).           |
