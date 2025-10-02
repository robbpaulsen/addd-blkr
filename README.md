# Un "Add Blocker" Sencillo y Efectivo

En la nueva Web 3 de Google, las extensiones famosas de "Add Blocker" ya han sido restringidas,
en el sentido de que fueron prohibidas de la "Google Play Store". Pero aun hay soluciones,
una de ellas siendo que por algun tiempo te instales un version estable de Google Chrome y 
evitar actualizar configurando las propias flags `chrome://flags` del navegador, pero esto
tiene sus riesgos y no hace muchos dias se publicaron un par de `0 days` muy fuertes 
en todos los navegadores que usan el `Chromium` web engine.

Segunda solucion y aun que no lo parezca o suene es escribir tu propia aplicacion/extension
"Add Blocker", leyendo la nueva estandarizacion de la `Web3` en el sitio de `Google Developers`
es muy sencillo y hasta el dia de hoy se pueden bloquear hasta un 70 - 80 % de los molestos anuncios
en paginas publicas, esto depende totalmente de la lista de reglas que tengas.

Y diras tu que eso es lo mismo que usar las extensiones de toda la vida, pero la verdad es que no. Mientras este pryecto solo aborda el tema desde esa perspectiva, ahora la extensibilidad de tu proyecto como "Ad Blocker" puede bloquear elementos de una url definida. Por ejemplo si ya conces lo que son tecnicas como `XSS` y conoces las convencionalidades con las cuales se implementa puede declararlo en tu tu archivo de reglas y a estos elementos no se les permite su ejecucion o funcionalidad. No digo que sea la cura del cancer pero si es algo muy diferente. 

*Abajo las imagenes cuando esta encendido y cuando no lo esta.*

## Alcance de este proyecto

Segun la documentacion de en "Google Developers" haciendo uso de la nueva funcion `chrome.declarativeNetRequest`
y de la funcion `chrome.declarativeContent`, se pueden bloquear "URL's" y propio contenido
que sirva una pagina, ejemplo el campo de "Subscribete a la Newsletter" de la pagina.

## Snippet parte del codigo:

### Manifest dot `json` (manifest.json):

```json
{
    "manifest_version": 3,
    "name": "Simple Ad Blocker",
    "version": "1.0.0",
    "permissions": [
        "declarativeNetRequest"
    ],
    "declarative_net_request": {
        "rule_resources": [
            {
                "id": "ruleset_1",
                "enabled": true,
                "path": "rules.json"
            }
        ]
    }
}
```

### Y aqui el snippet del rules dot `json` (rules.json)

```json
[
    {
        "id": 1,
        "priority": 1,
        "action": {
            "type": "block"
        },
        "condition": {
            "urlFilter": "*://*doubleclick.net/*"
        }
    },
    {
        "id": 2,
        "priority": 1,
        "action": {
            "type": "block"
        },
        "condition": {
            "urlFilter": "*://*googleadservices.com/*"
        }
    }
]
```

En el snippet solo se incluyen 2 ejemplos de URL's pero en el archivo que sera
usado ya en el navegador integra 11 URL's.


#### SCREENSHOT's

##### Desactivado
![](assets/unblocked-adds.png)

##### Activado
![](assets/blocked-adds.png)