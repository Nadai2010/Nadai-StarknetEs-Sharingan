# Paquete inicial de Sharingan

## Madara
[Madara](https://github.com/keep-starknet-strange/madara) es un secuenciador de Starknet.
Escrito en Rust y Substrate (un SDK para construir blockchain), Madara es un secuenciador impulsado por la comunidad
respaldado por el equipo Starkware Keep-Starknet-Strange, que se espera que sea uno de los principales secuenciadores que participen en la descentralización de Starknet.

Si no conoces Madara, echa un vistazo al repositorio y al [paquete inicial para contribuyentes](https://github.com/keep-starknet-strange/madara/blob/main/docs/contributor-starter-pack.md)
para tener una idea de cómo está construido.

Sin embargo, si solo quieres participar en Sharingan, puedes seguir leyendo esta guía,
que te guiará sin necesidad de conocimientos previos sobre Madara.


## ¿Qué es Sharingan?

Sharingan es una testnet efímera para Starknet en la que todas las nodos que participan en la red son instancias de Madara.
En esta testnet, Starknet se está probando de forma descentralizada, donde los nodos trabajan en consenso para determinar qué bloque se agrega a continuación en la cadena.

Pero también hay nodos que participan solo en el almacenamiento de datos, sin participar en el consenso.

Aunque Madara se llama "Secuenciador de Starknet", distinguimos dos tipos de nodos en Sharingan:

1. Madara como `secuenciador`, participando en el consenso.
2. Madara como `nodo completo` (fullnode), utilizado para la persistencia de datos.

Para el resto de la guía, "secuenciador" se referirá a una instancia de Madara que participa en el consenso,
y "nodo completo" se referirá a una instancia de Madara utilizada para la persistencia de datos.

El objetivo de Sharingan es comenzar a probar Starknet de forma descentralizada y también brindar acceso a todos para participar y probar la red de Starknet.

Para interactuar con la red de Starknet, los nodos de Starknet exponen un punto final JSON RPC. Esto significa que
cualquier instancia de Madara que participe en la red tendrá un puerto abierto para permitir la comunicación externa.
Más sobre esto en la sección dedicada a RPC.


## Tipología de Sharingan

Como se mencionó, Sharingan se basa en `secuenciadores` para producir, validar y agregar bloques a la cadena.

Hasta ahora, Sharingan tiene los siguientes `secuenciadores` conocidos:

| Mantenedor | ID | Alias de clave | IP | ID de par | Puerto RPC |
|------------|----|-----------|----|---------|----------|
| Starkware  | 1  | alice     | `52.7.206.208` | `12D3KooWJytWW4wqhG1xp9ckLb7B15KqDU24Q8HHo8VfwXmFe5ZE` | `9933` |
| Starkware  | 2  | bob     | `44.195.161.82` | `12D3KooWHocNfvLz6rgpb8wJsynSpMwkspkcRn6gmN5UiK1tTTeG` | `9933` |
| Cartridge  | 3  | charlie     | `208.67.222.222` | `12D3KooWQe2ZtqiyC5CLJKZr9i9xTmEyiAikZcr5J18w3cG1dQAc` | `9933` |
| LambdaClass  | 4  | dave     | `65.109.91.29` | `12D3KooWK8QhFjkGYGyMskDuCyaS1nrhfTfadMeRjJkox4SV32co` | `9933` |
| Pragma  | 5  | eve     | `13.39.22.82` | `12D3KooWGMCGJ517tFor12U9n2v3ax5WNw1pXFdj48hSHYQe6oyJ` | `9933` |
| Kakarot  | 6  | ferdie     | `52.50.242.182` | `12D3KooWHnQ8LC113DgB5cVVyx2mvTN7bBkm75zvzsndr2WhstEE` | `9933` |

Puedes encontrar más detalles técnicos en la discusión [aquí](https://github.com/keep-starknet-strange/madara/discussions/553).

Actualmente, Starkware elige los `secuenciadores`, y solo puedes unirte como un `fullnode`.

Como Madara está utilizando Substrate, existe una aplicación web existente que te permite monitorear el estado de Sharingan. Y para verificar la tipología del nodo, puedes ir directamente aquí a la pestaña de [información del nodo](https://starknet-madara.netlify.app/?rpc=wss%3A%2F%2Fsharingan.cartridge.gg/#/explorer/node).

Actualmente, los `secuenciadores` son elegidos por Starkware, y solo puedes unirte como un `fullnode`.

## Participar en Sharingan como un fullnode

Para participar en Sharingan, hay algunas consideraciones que debes tener en cuenta:

1. El código de Madara que ejecutarás deberá exponer dos puertos: uno para la comunicación entre pares, que actualmente es `30333`, y otro para la RPC mencionada anteriormente, que generalmente es `9933`.

2. Substrate utiliza `chain specs` para que todos los nodos participantes estén sincronizados en cómo colaborar en la red. La especificación de la cadena también es especial en Substrate, ya que incluye lo que llamamos el tiempo de ejecución, donde definimos cómo se procesan las transacciones dentro de los nodos.

Para participar en Sharingan como un `fullnode`, tienes dos opciones:

### Forma sencilla: imagen de Docker

Hay una imagen de Docker creada para Sharingan, que se actualizará en cada versión de Sharingan. Sin embargo, para asegurarte de que estás utilizando las "chain specs" correctas, sigue los siguientes pasos:

1. Descarga el [código fuente](https://github.com/keep-starknet-strange/madara/releases/tag/v0.1.0-testnet-sharingan-alpha.4) de la versión actual de la versión de Sharingan (actualmente `v0.1.0-testnet-sharingan-alpha.4`).

2. Extrae el archivo para acceder más tarde al archivo de interés, que es `madara/infra/chain-specs/testnet-sharingan-raw.json`.

3. Ejecuta el contenedor de Docker, donde utilizaremos 2 volúmenes. Uno para acceder al archivo de `chain specs` y otro para el almacenamiento de los datos de la cadena.

```bash
sudo docker run -v /tmp:/data \
                -v /ruta/a/madara/infra/chain-specs/:/chain-specs \
                ghcr.io/keep-starknet-strange/madara:v0.1.0-testnet-sharingan-alpha.4 \
                --chain /chain-specs/testnet-sharingan-raw.json \
                --base-path /data/sharingan \
                --bootnodes /ip4/52.7.206.208/tcp/30333/p2p/12D3KooWJytWW4wqhG1xp9ckLb7B15KqDU24Q8HHo8VfwXmFe5ZE \
                --rpc-cors=all \
                --rpc-external \
                --rpc-methods=unsafe \
                --port 30333 \
                --rpc-port 9933
```

Considera ejecutar el nodo en modo desconectado usando la opción `-d`. Pero primero intenta ejecutarlo sin la opción `-d`, ya que es más fácil ver qué sucede si es la primera vez que usas Docker.

### Forma de desarrollo: clonar el repositorio de Madara

Si prefieres tener Madara compilado localmente, debes:

1. Clonar el repositorio de [Madara](https://github.com/keep-starknet-strange/madara).
2. Hacer checkout en la etiqueta `v0.1.0-testnet-sharingan-alpha.4`.
3. Ejecutar `cargo build --workspace --release` (puedes consultar [esta guía](https://github.com/keep-starknet-strange/madara/blob/main/docs/rpc-contribution.md) con información sobre cómo compilar Madara).
4. Ejecutar el `fullnode` (en una ventana de terminal o cualquier otro método para mantenerlo en ejecución) desde la raíz del repositorio de Madara:

```bash
./target/release/madara \
--base-path /ruta/al/almacenamiento/sharingan \
--chain ./infra/chain-specs/testnet-sharingan-raw.json \
--bootnodes /ip4/52.7.206.208/tcp/30333/p2p/12D3KooWJytWW4wqhG1xp9ckLb7B15KqDU24Q8HHo8VfwXmFe5ZE \
--rpc-cors=all --rpc-external --rpc-methods=unsafe \
--port 30333 --rpc-port 9933
```

Una vez que tengas tu nodo en ejecución, puedes obtener tu Peer ID ejecutando el siguiente comando:

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
    "jsonrpc": "2.0",
    "method": "system_localPeerId",
    "params": [],
    "id": 1
}' \
http://tu_ip:9933
```

Luego puedes ir al [explorador de nodos](https://starknet-madara.netlify.app/?rpc=wss%3A%2F%2Fsharingan.cartridge.gg/#/explorer/node) y verificar que tu nodo aparezca y comience a sincronizar los bloques.

¡Bienvenido a Sharingan, estás dentro! :rocket:

Por ahora, hay pocas transacciones y el almacenamiento para los más de 20,000 bloques es inferior a 1 GB. Pero esto variará en el futuro dependiendo de la actividad de la red.

## Interactuar con Starknet utilizando JSON RPC

Para interactuar con Starknet utilizando un nodo de Sharingan, debes usar JSON RPC directamente (con comandos como `curl`) o indirectamente utilizando programas CLI de Starknet como [starkli](https://github.com/xJonathanLEI/starkli) (Próximamente se proporcionará documentación sobre starkli).

Actualmente, Madara aún está en desarrollo activo y se recomienda consultar regularmente la [página de compatibilidad de características de Starknet de Madara](https://github.com/keep-starknet-strange/madara/blob/v0.1.0-testnet-sharingan-alpha.4/docs/starknet_features_compatibility.md).

En la versión actual, **por favor, no uses** puntos finales de RPC no admitidos, ya que estamos trabajando en manejarlos.

Aquí tienes algunos ejemplos de RPC utilizando el secuenciador-1 de Starkware:

### Obtener el hash del último bloque:

```bash
starkli block-hash --rpc http://52.7.206.208:9933
```

Este comando utiliza la herramienta `starkli` para obtener el hash del último bloque en el nodo de Sharingan. Se realiza una solicitud al endpoint RPC `http://52.7.206.208:9933` y se obtiene el hash del bloque.

```bash
curl --header "Content-Type: application/json" \
     --request POST \
     --data '{
     "jsonrpc": "2.0",
     "method": "starknet_blockHashAndNumber",
     "params": ["latest"],
     "id":1}' \
     http://52.7.206.208:9933
```

Este comando utiliza `curl` para enviar una solicitud JSON RPC y obtener el hash y el número del último bloque en el nodo de Sharingan. La respuesta contendrá la información solicitada.

## Explorador de Substrate de Sharingan

[Aquí](https://starknet-madara.netlify.app/?rpc=wss%3A%2F%2Fsharingan.cartridge.gg/#/explorer/node) se encuentra la aplicación web para visualizar el estado de Sharingan.

Como se mencionó anteriormente, Madara utiliza el SDK de Substrate. Como particularidad de cómo Madara utiliza Substrate, cualquier bloque de Starknet se produce y se envuelve en un bloque de Substrate.

Los bloques de Substrate no utilizan el mismo método de hash que Starknet. Por esta razón, los bloques visibles en el explorador no coinciden con los bloques que se pueden ver en exploradores de Starknet como starkscan o voyager.

Pero esta es una excelente herramienta para verificar la tipología de Sharingan y la producción de bloques.

## ¿Qué puedo hacer en Sharingan?

Por ahora, Madara (y luego Sharingan) no admiten Cairo 1, ¡pero esto llegará pronto!

La idea es que muchas personas utilicen Sharingan como una red de prueba, implementen contratos y envíen transacciones a los nodos de Sharingan.

Esta será la forma más efectiva de iniciar la descentralización de Starknet.

Por ahora, puedes tomar contratos existentes de Cairo 0 y probarlos en Sharingan, ¡pero prepárate! Quantum Leap se acerca y ¡Madara no se queda atrás...! :rocket:

¡Sigamos construyendo y gracias por ser parte o tener interés en la red de prueba Sharingan!