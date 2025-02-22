# Taller de Programacion

## Grupo

Nombre del grupo: **"Los Raviolines"**

- Rodolfo Valentin Albornoz Tomé (107975)
- Francisco Antonio Pereyra (105666)

## Como usar

### Iniciar Servidor de NATS

```bash
# Valores por defecto
cargo run --bin messaging-server
# Parámetros de configuración
cargo run --bin messaging-server -- puerto=4222 direccion=0.0.0.0 cuentas=users.csv
# Archivo de configuración
cargo run --bin messaging-server -- config=config.txt
# Mixto
cargo run --bin messaging-server -- puerto=4222 config=config.txt
```

**Configuración: config.txt**
```txt
puerto=4222
direccion=0.0.0.0
cuentas=users.csv
```

**Cuentas: users.csv**
```csv
1,admin,1234
2,usuario,1234
```

### Iniciar Sistema Central de Cámaras

```bash
# Valores por defecto
cargo run --bin cameras
# Parámetros de configuración
cargo run --bin cameras -- direccion=localhost puerto=4222 camaras=camaras.csv
# Archivo de configuración
cargo run --bin cameras -- config=config.txt
```

### Iniciar App de Monitoreo

Antes de ejecutar el monitoreo, se debe tener en cuenta que el sistema central de cámaras y el servidor de mensajería deben estar corriendo.

Si se utiliza Linux se deben instalar algunas dependencias para que funcione la librería de UI:
```bash
sudo apt update -y && sudo apt-get install -y libclang-dev libgtk-3-dev libxcb-render0-dev libxcb-shape0-dev libxcb-xfixes0-dev libxkbcommon-dev libssl-dev
```

```bash
# Valores por defecto
cargo run --bin monitoring
# Parámetros de configuración
cargo run --bin monitoring -- direccion=localhost puerto=4222
# Archivo de configuración
cargo run --bin monitoring -- config=config.txt
```

### Iniciar Agente (Dron)

El Agente se debe iniciar luego de que este corriendo la App de Monitoreo. Cada Agente se inicia individualmente, es decir, no pueden iniciarse mas de uno en una sola corrida.

```bash
# Parámetros de configuración
cargo run --bin drone id=1 latitud=-34.617943832031656 longitud=-58.381372092491766 rango=800 velocidad=60 duracion_bateria=120 duracion_bateria_minima=30 tiempo_recarga=6 tiempo_atender_incidente=5
# Archivo de configuración .txt
cargo run --bin drone config=config.txt
# Archivo de configuración .csv
cargo run --bin drone id=1 drones=drones.csv
# Mixto
cargo run --bin drone id=1 config=config.txt
```

**Configuración: config.txt**
```txt
id=1
latitud=-34.617943832031656
longitud=-58.381372092491766
rango=800
velocidad=60
duracion_bateria=120
duracion_bateria_minima=30
tiempo_recarga=6
tiempo_atender_incidente=5
```

**Configuración: drones.csv**
```csv
1,-34.617943832031656,-58.381372092491766,800,60,120,30,6,5
2,-34.625032227138014,-58.38792059542602,600,40,140,40,5,4
```

## Como testear

`cargo test`

Para testear un paquete en particular:
`cargo test --bin <nombre>`