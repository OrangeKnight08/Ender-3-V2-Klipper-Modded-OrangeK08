# 🖨️ Ender 3 V2 Klipper Modded — OrangeK08

![Klipper](https://img.shields.io/badge/Firmware-Klipper-blue)
![Mainsail](https://img.shields.io/badge/Interface-Mainsail-red)
![Moonraker](https://img.shields.io/badge/API-Moonraker-purple)
![Ender 3 V2](https://img.shields.io/badge/Printer-Ender%203%20V2-black)
![SKR Mini E3 V3](https://img.shields.io/badge/Board-SKR%20Mini%20E3%20V3.0-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

Projeto pessoal da minha **Creality Ender 3 V2 altamente modificada**, utilizando **Klipper + Mainsail + Moonraker**.

Este repositório reúne as configurações, modificações, calibrações e automações utilizadas atualmente na minha impressora.

O objetivo do projeto é explorar o potencial da Ender 3 V2, buscando **mais velocidade, aceleração, qualidade, precisão, confiabilidade e automação**.

---

# 📸 Minha Ender 3 V2

<p align="center">
  <img src="images/ender3v2-main.jpg" alt="Ender 3 V2 Klipper Modded OrangeK08" width="700">
</p>

<p align="center">
  <i>Minha Ender 3 V2 modificada rodando Klipper dentro do enclosure.</i>
</p>

> ⚠️ **IMPORTANTE:** Esta configuração foi desenvolvida e calibrada especificamente para a minha impressora.
>
> Utilize este projeto como referência. Antes de utilizar qualquer configuração em outra máquina, revise pinagem, limites, correntes, offsets e faça suas próprias calibrações.

---

# 🔧 Especificações principais

| Componente | Configuração |
|---|---|
| Impressora | Creality Ender 3 V2 |
| Firmware | Klipper |
| Interface | Mainsail |
| API | Moonraker |
| Placa-mãe | BIGTREETECH SKR Mini E3 V3.0 |
| MCU | STM32G0B1 |
| Drivers | TMC2209 |
| Cinemática | Cartesian |
| Host | PC Linux |
| Extrusor | BMG Clone Direct Drive |
| Hotend | TZ E3 2.0 |
| Nivelamento | CR Touch |
| Sensor de filamento | BTT SFS V2 |
| Input Shaper | ADXL345 |

---

# 🛠️ Principais modificações

Minha Ender 3 V2 possui diversas modificações mecânicas e eletrônicas:

- Linear Rail MGN12H no eixo X
- Linear Rail no eixo Y
- Dual Z
- Dois motores no eixo Z
- Estabilização superior do eixo Z
- Direct Drive
- Extrusor BMG Clone
- Hotend TZ E3 2.0
- Hero Me modificado
- CR Touch
- BTT Smart Filament Sensor V2
- ADXL345 para Input Shaper
- Enclosure Creality
- Iluminação LED interna
- Refrigeração modificada da eletrônica
- Dissipadores nos motores
- Ventoinha maior para a placa-mãe
- Ventoinha de 120 mm na fonte
- Isolamento térmico sob a mesa
- Reguladores metálicos da mesa
- Superfície magnética de impressão

---

# ⚙️ Movimento

A máquina recebeu modificações importantes nos eixos X, Y e Z.

## 🛤️ Eixo X

- Linear Rail MGN12H
- Toolhead montado no sistema de trilho linear
- Hero Me
- Direct Drive

## 🛤️ Eixo Y

- Linear Rail
- Sistema de movimentação da mesa modificado

## ⚙️ Eixo Z

- Dual Z
- Dois motores
- Estabilização superior

---

# 🚀 Configuração atual de movimento

Configuração atualmente utilizada no `printer.cfg`:

```ini
[printer]
kinematics: cartesian
max_velocity: 250
max_accel: 4000
max_z_velocity: 15
square_corner_velocity: 5.0
max_z_accel: 300
```

| Parâmetro | Valor |
|---|---:|
| Velocidade máxima | **250 mm/s** |
| Aceleração máxima | **4000 mm/s²** |
| Square Corner Velocity | **5.0 mm/s** |
| Velocidade máxima Z | **15 mm/s** |
| Aceleração máxima Z | **300 mm/s²** |

---

# 📐 Limites dos eixos

| Eixo | Limite |
|---|---:|
| X | **250 mm** |
| Y | **230 mm** |
| Z | **250 mm** |

Configuração:

```ini
[stepper_x]
position_max: 250
homing_speed: 75

[stepper_y]
position_max: 230
homing_speed: 75

[stepper_z]
position_max: 250
position_min: -6
```

---

# 🧩 Hero Me / Toolhead

A impressora utiliza um **Hero Me modificado** como conjunto do toolhead.

O sistema integra:

- Hero Me
- Direct Drive
- BMG Clone
- Hotend TZ E3 2.0
- CR Touch
- Refrigeração do Hotend
- Refrigeração da peça
- Montagem no Linear Rail do eixo X

O objetivo desse conjunto é melhorar a integração entre o sistema de extrusão, refrigeração, sensor de nivelamento e movimentação do eixo X.

---

# 🔥 Extrusor

A máquina utiliza **BMG Clone em Direct Drive**.

### Configuração atual

```ini
[extruder]
microsteps: 16
rotation_distance: 7.4
nozzle_diameter: 0.400
filament_diameter: 1.750
```

### Driver

```ini
[tmc2209 extruder]
run_current: 0.650
```

### Características

- BMG Clone
- Direct Drive
- TMC2209
- Rotation Distance: **7.4**
- Corrente configurada: **0.650 A**
- Filamento: **1.75 mm**

O Direct Drive também facilita a utilização de materiais flexíveis como TPU.

---

# 🔥 Hotend

A impressora utiliza:

**TZ E3 2.0**

Configuração:

- Bico: **0.4 mm**
- Temperatura máxima configurada: **300 °C**
- Termistor: **EPCOS 100K B57560G104F**

```ini
sensor_type: EPCOS 100K B57560G104F
min_temp: 0
max_temp: 300
```

---

# 📏 CR Touch

O nivelamento utiliza **CR Touch** como `z_virtual_endstop`.

Configuração atual:

```ini
[bltouch]
sensor_pin: ^PC14
control_pin: PA1
x_offset: -52
y_offset: -11
speed: 10
samples: 3
samples_result: median
sample_retract_dist: 2.0
samples_tolerance: 0.02
samples_tolerance_retries: 3
```

## Safe Z Home

```ini
[safe_z_home]
home_xy_position: 160,120
speed: 250
z_hop: 7
z_hop_speed: 10
```

O Z Offset deve ser calibrado individualmente para cada máquina.

---

# 🛏️ Bed Mesh

A configuração atualmente salva utiliza uma malha:

**5 × 5**

Área:

- X: **30 → 195 mm**
- Y: **40 → 200 mm**
- Algoritmo: **Bicubic**

Também utilizo recursos de **Adaptive Bed Mesh** através das configurações e macros da máquina.

---

# 📊 ADXL345 + Input Shaper

A máquina utiliza **BTT ADXL345 V2.0 / RP2040** para análise de ressonância.

O acelerômetro é utilizado para:

- Medir vibrações
- Calibrar o eixo X
- Calibrar o eixo Y
- Configurar Input Shaper
- Reduzir ringing
- Reduzir ghosting
- Otimizar velocidade e aceleração

A configuração do ADXL pode ser ativada quando necessária:

```ini
#[include ADXL345.cfg]
```

---

# 📈 Input Shaper

Configuração atual:

```ini
[input_shaper]
shaper_type_x: 3hump_ei
shaper_freq_x: 77.2
shaper_type_y: mzv
shaper_freq_y: 39
```

### Eixo X

**3HUMP_EI @ 77.2 Hz**

### Eixo Y

**MZV @ 39 Hz**

> Estes valores são específicos da configuração atual da minha impressora e não devem ser simplesmente copiados para outra máquina.

---

# 🧵 BTT Smart Filament Sensor V2

A impressora utiliza o **BIGTREETECH Smart Filament Sensor V2 (SFS V2)**.

O sistema monitora tanto a presença quanto o movimento do filamento.

### Sensores

- Filament Switch Sensor
- Filament Motion Sensor
- Encoder de movimento

### Recursos

- Detecção de presença do filamento
- Detecção de falta de filamento
- Detecção de movimento
- Detecção de possível travamento
- Pausa automática da impressão

A configuração fica no arquivo:

```text
btt-sfs-v2.cfg
```

---

# 🌡️ Monitoramento de temperatura

A máquina possui monitoramento de:

- Hotend
- Mesa aquecida
- MCU
- PC/Host Klipper

### MCU

```ini
[temperature_sensor MCU]
sensor_type: temperature_mcu
```

### PC

```ini
[temperature_sensor PC]
sensor_type: temperature_host
min_temp: 10
max_temp: 100
```

---

# 🛏️ Mesa aquecida

Configuração da mesa:

- Termistor EPCOS 100K B57560G104F
- Controle PID
- Temperatura máxima configurada: **130 °C**
- Isolamento térmico sob a mesa
- Reguladores metálicos
- Sistema de regulagem modificado
- Superfície magnética de impressão

---

# ❄️ Refrigeração

O Klipper controla:

- Part Cooling Fan
- Heatbreak Cooling Fan
- Controller Fan

A máquina também recebeu melhorias físicas de refrigeração:

- Ventoinha de **60 × 20 mm** na região da placa-mãe
- Dissipadores nos motores
- Ventilação modificada da eletrônica
- Ventoinha de **120 mm** na fonte

---

# 🏠 Enclosure

A impressora funciona dentro de um **enclosure Creality**.

O enclosure possui iluminação interna e auxilia principalmente na estabilidade térmica durante impressões com materiais que se beneficiam de um ambiente mais controlado.

Temperaturas internas observadas em algumas impressões ficam aproximadamente na faixa de:

**35–37 °C**

---

# 🧪 Filamentos utilizados

A máquina é utilizada com:

- PLA
- PETG
- ABS
- TPU

Cada material possui perfis específicos de:

- Temperatura
- Velocidade
- Ventilação
- Flow
- Retração
- Pressure Advance

---

# 🎯 Calibrações

Ao longo do projeto são realizadas calibrações de:

- PID do Hotend
- PID da mesa
- Rotation Distance
- Flow
- Pressure Advance
- Input Shaper
- Ressonância
- CR Touch
- Z Offset
- Probe Accuracy
- Bed Mesh
- Retração
- Precisão dimensional
- Velocidade
- Aceleração

As calibrações podem ser atualizadas conforme novos upgrades são instalados.

---

# 🤖 Klipper e automações

A configuração utiliza recursos como:

- Klipper
- Mainsail
- Moonraker
- Macros personalizadas
- Adaptive Bed Mesh
- Input Shaper
- Pressure Advance
- BTT SFS V2
- Timelapse
- Exclude Object
- Pause / Resume
- Skew Correction
- Force Move
- Shell Commands
- Monitoramento de temperatura
- Som ao finalizar impressão
- Rotinas personalizadas de início e término de impressão

---

# 📂 Arquivos de configuração

O projeto utiliza vários arquivos `.cfg`.

### `printer.cfg`

Configuração principal da impressora.

### `macro.cfg`

Macros personalizadas.

### `btt-sfs-v2.cfg`

Configuração do BTT Smart Filament Sensor V2.

### `timelapse.cfg`

Configuração do Timelapse.

### `shell_command.cfg`

Comandos Shell e automações.

### `ADXL345.cfg`

Configuração utilizada para calibração com o acelerômetro.

---

# 📁 Estrutura do repositório

```text
Ender-3-V2-Klipper-Modded-OrangeK08/
│
├── README.md
├── LICENSE
│
├── printer.cfg
├── macro.cfg
├── btt-sfs-v2.cfg
├── timelapse.cfg
├── shell_command.cfg
├── ADXL345.cfg
│
├── images/
│   ├── ender3v2-main.jpg
│   ├── hero-me.jpg
│   ├── linear-rail-x.jpg
│   ├── linear-rail-y.jpg
│   └── electronics.jpg
│
└── calibration/
    └── resultados de calibração
```

---

# 📄 printer.cfg

O arquivo principal pode ser encontrado em:

[`printer.cfg`](./printer.cfg)

Ele contém:

- MCU
- Cinemática
- Limites de movimento
- Steppers X/Y/Z
- TMC2209
- Extrusor
- Hotend
- Mesa aquecida
- Fans
- CR Touch
- Safe Z Home
- Input Shaper
- Sensores de temperatura
- Board Pins
- Skew Correction

Os outros arquivos são carregados através de `[include]`.

---

# 📸 Galeria

Conforme o projeto evoluir, serão adicionadas fotos detalhadas das modificações.

## 🖨️ Visão geral

<p align="center">
  <img src="images/ender3v2-main.jpg" alt="Ender 3 V2 Modded" width="600">
</p>

## 🧩 Hero Me / Toolhead

<!-- Quando adicionar a foto hero-me.jpg, remova este comentário.

![Hero Me](images/hero-me.jpg)

-->

## 🛤️ Linear Rail X

<!-- Quando adicionar a foto linear-rail-x.jpg, remova este comentário.

![Linear Rail X](images/linear-rail-x.jpg)

-->

## 🛤️ Linear Rail Y

<!-- Quando adicionar a foto linear-rail-y.jpg, remova este comentário.

![Linear Rail Y](images/linear-rail-y.jpg)

-->

## 🧠 Eletrônica

<!-- Quando adicionar a foto electronics.jpg, remova este comentário.

![Eletrônica](images/electronics.jpg)

-->

---

# 🚀 Objetivos do projeto

O objetivo é continuar evoluindo a Ender 3 V2 para alcançar:

- 🚀 Maior velocidade
- ⚡ Maior aceleração
- 🎯 Maior precisão
- 🖨️ Melhor qualidade de impressão
- 📉 Menos ringing e ghosting
- 🔧 Maior confiabilidade
- 🌡️ Melhor controle térmico
- 🤖 Mais automação
- 📊 Melhor monitoramento
- 🧵 Maior confiabilidade na alimentação do filamento

Este projeto está em constante evolução.

---

# ⚠️ Aviso importante

**NÃO copie o `printer.cfg` diretamente para outra impressora sem revisar a configuração.**

Antes de utilizar qualquer configuração deste repositório, verifique:

- Placa-mãe
- MCU
- Serial da MCU
- Pinagem
- Drivers
- Corrente dos motores
- Direção dos motores
- Endstops
- Dimensões da máquina
- Limites dos eixos
- CR Touch / BLTouch
- Z Offset
- Hotend
- Termistores
- PID
- Rotation Distance
- Input Shaper
- Pressure Advance
- Sensores de filamento

Uma configuração incorreta pode provocar movimentos inesperados, colisões ou danos ao equipamento.

**Use este projeto como referência e realize suas próprias calibrações.**

---

# 📜 Licença

Este projeto é disponibilizado sob a **MIT License**.

Você pode utilizar, estudar, modificar e compartilhar o conteúdo conforme os termos da licença.

Consulte:

[`LICENSE`](./LICENSE)

---

# 👤 Autor

**OrangeKnight08 — OrangeK08**

Projeto pessoal de modificação e evolução da **Creality Ender 3 V2**.

⭐ Se este projeto ajudar na sua própria Ender 3 V2, considere deixar uma estrela no repositório.

---

### 🔧 Projeto em constante evolução

Novos upgrades, calibrações, fotos e configurações serão adicionados conforme a máquina continuar evoluindo.
