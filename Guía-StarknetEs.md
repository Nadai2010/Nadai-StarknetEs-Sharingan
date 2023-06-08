<div align="center">
<img alt="starknet logo" src="imágenes/Madara.jpg" width="600" >
  <h1 style="font-size: larger;">
    <img src="https://github.com/Nadai2010/Nadai-SHARP-Starknet/blob/master/im%C3%A1genes/Starknet.png" width="40">
    <strong>Madara RPC-Testnet Sharingan</strong> 
    <img src="https://github.com/Nadai2010/Nadai-SHARP-Starknet/blob/master/im%C3%A1genes/Starknet.png" width="40">
  </h1>
</div>

# Madara 🥷 
Madara es un secuenciador Starknet estándar, personalizable y increíblemente rápido ⚡ diseñado para hacer que sus proyectos se disparen

Construido sobre el robusto marco del Substrate y rápido, gracias a Rust, Madara ofrece un rendimiento y escalabilidad inigualables para alimentar su cadena de Validity Roolup basada en Starknet.

## Testnet Sharingan-alpha.4
En esta guía aprenderemos cómo conectar a una RPC de [Madara](https://github.com/keep-starknet-strange/madara) y utilizar sus llamadas desde la línea de comandos. Para probar y explorar todas las funcionalidades de Madara, contamos con la testnet [Sharingan](https://github.com/keep-starknet-strange/madara/discussions/553).

Madara nos permite sumergirnos en un mundo de descentralización. Además de actuar también como un nodo completo, podemos utilizar Sharingan para realizar consultas a través de la RPC, si quiere aprender más sobre Madara, consulte sus [doc oficiales](https://docs.madara.wtf/)

Con Madara y la futura capa L3 de Starknet, se abren un sinfín de posibilidades para cualquier persona interesada en la descentralización. 

Para explorar y poner a prueba Sharingan, puedes acceder al [explorador de la testnet](https://starknet-madara.netlify.app/?rpc=wss%3A%2F%2Fsharingan.cartridge.gg%2F#/explorer). Desde allí, podrás consultar y experimentar con todas las llamadas disponibles en Madara.

¡Únete a esta aventura en la descentralización con Madara y comienza a descubrir un nuevo mundo de posibilidades!

## Sharingan RPC

1. Clonar repo oficial de Madara:
```bash
gh repo clone keep-starknet-strange/madara
```

2. Construir las dependencias y ajustes necesarios en Madara, para ello navegaremos dentro de la carpeta `madara` que hemos clonado y haremos el build:

```bash
cargo build --workspace --release
```

![Graph](/im%C3%A1genes/build.png)


3. Aquí es posible que te encuentres con algunos errores debido a la falta de dependencias. Puedes consultar la sección de errores para obtener más información sobre cómo solucionarlos.

Además, es importante tener en cuenta que el tiempo de procesamiento puede variar dependiendo de la potencia de hardware y otras características de tu dispositivo. En mi caso, el proceso con el número `1048` tardó aproximadamente `15 minutos`, mientras que el proceso con el número `1055` tomó alrededor de `20 minutos`. En general, en dispositivos de gama baja o media, es posible que debas esperar aproximadamente 50 minutos en total. También ten en cuenta que se ha requerido aproximadamente 6.5 GB de espacio en la carpeta de utilidades.

Una vez que la construcción de Madara haya finalizado, podrás ejecutar varios comandos. En este caso, lanzaremos el siguiente comando para conectarnos a la RPC y llamar al método `starknet_blockHashAndNumber` utilizando el operador de Starkware. Puedes consultar la sección de operadores para obtener más información sobre los operadores disponibles y cómo conectar con ellos.

Recuerda que es importante tener paciencia durante el proceso y consultar la documentación para obtener más detalles sobre cada paso. 

¡Buena suerte en tu experiencia con Madara!


```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_blockHashAndNumber",
    "params": [],
    "id":1
}' http://52.7.206.208:9933
```
![Graph](/im%C3%A1genes/hashnumber.png)

## Operadores
Para una iformación más detallada consulte Debate sobre [Sharingan](https://github.com/keep-starknet-strange/madara/discussions/553)

| Mantenedor | ID | Alias de clave | IP | ID de par | Puerto RPC |
|------------|----|-----------|----|---------|----------|
| Starkware  | 1  | alice     | `52.7.206.208` | `12D3KooWJytWW4wqhG1xp9ckLb7B15KqDU24Q8HHo8VfwXmFe5ZE` | `9933` |
| Starkware  | 2  | bob     | `44.195.161.82` | `12D3KooWHocNfvLz6rgpb8wJsynSpMwkspkcRn6gmN5UiK1tTTeG` | `9933` |
| Cartridge  | 3  | charlie     | `208.67.222.222` | `12D3KooWQe2ZtqiyC5CLJKZr9i9xTmEyiAikZcr5J18w3cG1dQAc` | `9933` |
| LambdaClass  | 4  | dave     | `65.109.91.29` | `12D3KooWK8QhFjkGYGyMskDuCyaS1nrhfTfadMeRjJkox4SV32co` | `9933` |
| Pragma  | 5  | eve     | `13.39.22.82` | `12D3KooWGMCGJ517tFor12U9n2v3ax5WNw1pXFdj48hSHYQe6oyJ` | `9933` |
| Kakarot  | 6  | ferdie     | `52.50.242.182` | `12D3KooWHnQ8LC113DgB5cVVyx2mvTN7bBkm75zvzsndr2WhstEE` | `9933` |

## Errores

A continuación, se presentan algunos errores comunes que debes tener en cuenta durante la construcción del proyecto:

1. **Rutas y espacios incorrectos**: Es importante asegurarse de que las rutas y los nombres de las carpetas estén escritos correctamente, ya que cualquier error en este aspecto puede ocasionar problemas en la construcción del proyecto. Por ejemplo:
   - **Incorrecto**: Nadai-StarknetEs Madara
   - **Correcto**: Nadai-StarknetEs-Madara

2. **Error en la ruta de LIBCLANG**: En algunos casos, puede haber problemas con la ruta de LIBCLANG. Para verificar la ruta actual, puedes utilizar el siguiente comando en la terminal:
   ```bash
   ldconfig -p | grep libclang
   ```
   Si solo se muestra la ruta del sistema y algunas más, es posible que debas instalar y actualizar las dependencias necesarias. Puedes hacerlo ejecutando el siguiente comando:
   ```bash
   sudo apt-get update && sudo apt-get install -y clang llvm libudev-dev protobuf-compiler
   ```
   Luego, puedes intentar compilar nuevamente utilizando el comando:
   ```bash
   cargo build --workspace --release
   ```
   Si aún encuentras errores relacionados con CLANG, es posible que debas identificar la ruta del nuevo CLANG instalado e exportarla utilizando el siguiente comando:
   ```bash
   export LIBCLANG_PATH=/ruta/nueva/de/clang/
   ```

3. **Error de dependencia Protoc**: En caso de que el error esté relacionado sólo con Protoc, puedes intentar instalar el paquete necesario utilizando el siguiente comando:
   ```bash
   sudo apt-get install protobuf-compiler
   ```

4. **Reiniciar o limpiar la compilación**: Si experimentas problemas persistentes, puedes reiniciar o limpiar la compilación para empezar de nuevo sin tener que eliminar la carpeta del proyecto por completo. Puedes utilizar el siguiente comando de cargo para eliminar solo los datos de compilación:
   ```bash
   cargo clean
   ```

Recuerda que estos son solo algunos ejemplos de errores comunes y sus posibles soluciones. 

Siempre es recomendable revisar la documentación y consultar la comunidad en caso de encontrar problemas específicos durante la construcción del proyecto.

## Comandos

| Feature                                  | State              |
| ---------------------------------------- | ------------------ |
| starknet_getBlockWithTxHashes            | :white_check_mark: |
| starknet_getBlockWithTxs                 | :white_check_mark: |
| starknet_getStateUpdate                  | :construction:     |
| starknet_getStorageAt                    | :white_check_mark: |
| starknet_getTransactionByHash            | :white_check_mark: |
| starknet_getTransactionByBlockIdAndIndex | :white_check_mark: |
| starknet_getTransactionReceipt           | :white_check_mark: |
| starknet_getClass                        | :white_check_mark: |
| starknet_getClassHashAt                  | :white_check_mark: |
| starknet_getClassAt                      | :white_check_mark: |
| starknet_getBlockTransactionCount        | :white_check_mark: |
| starknet_call                            | :white_check_mark: |
| starknet_estimateFee                     | :white_check_mark: |
| starknet_blockNumber                     | :white_check_mark: |
| starknet_blockHashAndNumber              | :white_check_mark: |
| starknet_chainId                         | :white_check_mark: |
| starknet_pendingTransactions             | :white_check_mark: |
| starknet_syncing                         | :white_check_mark: |
| starknet_getEvents                       | :white_check_mark: |
| starknet_getNonce                        | :white_check_mark: |
| starknet_traceTransaction                | :construction:     |
| starknet_simulateTransaction             | :construction:     |
| starknet_traceBlockTransactions          | :construction:     |
| starknet_addInvokeTransaction            | :white_check_mark: |
| starknet_addDeclareTransaction           | :white_check_mark: |
| starknet_addDeployAccountTransaction     | :white_check_mark: |

## Bloques y Hash

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_getBlockWithTxHashes",
    "params": [
        "latest"
    ],
    "id":1
}' http://52.7.206.208:9933
```
![Graph](/im%C3%A1genes/blocktxhash.png)

## Ultimo bloque y Hash

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_blockHashAndNumber",
    "params": [],
    "id":1
}' http://52.7.206.208:9933
```

![Graph](/im%C3%A1genes/hashnumber.png)

### Ultimo Bloque

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_blockNumber",
    "params": [],
    "id":1
}' http://52.7.206.208:9933
```

![Graph](/im%C3%A1genes/blocknumber.png)

## Chain ID

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_chainId",
    "params": [],
    "id":1
}' http://52.7.206.208:9933
```

![Graph](/im%C3%A1genes/chainid.png)

En este `0x534e5f474f45524c49` caso la traduccion en hezadecimal es SNGOERLI.

## Transaciones pendientes

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
    "jsonrpc": "2.0",
    "method": "starknet_syncing",
    "params": [],
    "id":1
}' http://52.50.242.182:9933
```

![Graph](/im%C3%A1genes/sync.png)

## Bloques y Tx

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_getBlockWithTxs",
    "params": [
        "latest"
    ],
    "id":1
}' http://52.7.206.208:9933
```

## Contador de Transacciones en Bloque

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_getBlockTransactionCount",
    "params": [
        "latest"
    ],
    "id":1
}' http://52.7.206.208:9933
```

## Get Class

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_getClass",
    "params": [
        "latest"
        "0x00d0e183745e9dae3e4e78a8ffedcce0903fc4900beace4e0abf192d4c202da3"
    ],
    "id":1
}' http://52.7.206.208:9933
```

## State Update

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
   "jsonrpc": "2.0",
    "method": "starknet_getStateUpdate",
    "params": [
        "latest"
    ],
    "id":1
}' http://52.7.206.208:9933
```

## Transacción por Hash 

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{
    "jsonrpc": "2.0",
    "method": "starknet_getTransactionByHash",
    "params": [
        "0x89be401f95ef765e78bc6485905c5b62de53818dc46d622460faf5f5cef0d7"
    ],
    "id":1
}' http://52.50.242.182:9933
```

