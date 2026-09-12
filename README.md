# 🖨️ Ender 3 V2 Klipper Modded — OrangeK08

![Klipper](https://img.shields.io/badge/Firmware-Klipper-blue)
![Board](https://img.shields.io/badge/Board-BTT%20SKR%20Mini%20E3%20V3.0-green)
![Printer](https://img.shields.io/badge/Printer-Ender%203%20V2-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

Projeto pessoal da minha **Creality Ender 3 V2 altamente modificada**, utilizando **Klipper, Mainsail e Moonraker**.

Este repositório reúne as configurações, modificações, calibrações e automações que utilizo atualmente na impressora.

O objetivo do projeto é explorar o potencial da Ender 3 V2, buscando **mais velocidade, aceleração, qualidade, precisão e confiabilidade**, sem abandonar a plataforma original da máquina.

> ⚠️ **IMPORTANTE:** Esta configuração foi desenvolvida e calibrada especificamente para a minha impressora.  
> Use este projeto como referência e revise todas as configurações antes de aplicá-las em outra máquina.

---

# 🔧 Hardware

## 🖨️ Impressora

- Creality Ender 3 V2
- Klipper Firmware
- Mainsail
- Moonraker
- PC Linux dedicado como host Klipper

## 🧠 Placa-mãe

- BIGTREETECH SKR Mini E3 V3.0
- MCU STM32G0B1
- Drivers TMC2209

---

# ⚙️ Movimento

A estrutura original da Ender 3 V2 recebeu diversas modificações no sistema de movimento.

### Upgrades

- 🛤️ Linear Rail no eixo X
- 🛤️ Linear Rail no eixo Y
- ⚙️ Dual Z
- ⚙️ Dois motores no eixo Z
- 🔩 Estabilização superior do eixo Z
- 🔧 Estrutura modificada

### Configuração atual do Klipper

| Parâmetro | Valor |
|---|---:|
| Velocidade máxima | **250 mm/s** |
| Aceleração máxima | **4000 mm/s²** |
| Square Corner Velocity | **5.0 mm/s** |
| Velocidade máxima Z | **15 mm/s** |
| Aceleração máxima Z | **300 mm/s²** |

### Limites configurados

| Eixo | Limite |
|---|---:|
| X | **250 mm** |
| Y | **230 mm** |
| Z | **250 mm** |

---

# 🔥 Extrusor e Hotend

A impressora utiliza sistema **Direct Drive**.

### Hardware

- Direct Drive
- Extrusor BMG Clone
- Hotend TZ E3 2.0
- Bico de **0.4 mm**
- Filamento de **1.75 mm**

### Configuração atual

```ini
rotation_distance: 7.4
nozzle_diameter: 0.400
filament_diameter: 1.750
```

Driver do extrusor:

```ini
run_current: 0.650
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

### Safe Z Home

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

A configuração salva atualmente utiliza uma malha:

**5 × 5**

Área:

- X: **30 → 195 mm**
- Y: **40 → 200 mm**

Algoritmo:

`bicubic`

A malha pode mudar conforme novas calibrações forem realizadas.

---

# 📊 Input Shaper

A impressora utiliza Input Shaper para reduzir vibração, ringing e ghosting.

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

Os valores foram obtidos para esta configuração específica da máquina e não devem ser simplesmente copiados para outra impressora.

---

# 🧵 BTT Smart Filament Sensor V2

A impressora utiliza o **BIGTREETECH Smart Filament Sensor V2 (SFS V2)**.

O sistema monitora não apenas a presença do filamento, mas também seu movimento.

### Recursos

- Detecção de presença de filamento
- Sensor Switch
- Sensor de movimento
- Encoder
- Detecção de falta de filamento
- Detecção de possível travamento do filamento
- Pausa automática da impressão

A configuração do sensor fica separada em:

```text
btt-sfs-v2.cfg
```

---

# 📈 ADXL345

A máquina também utiliza acelerômetro para calibração de ressonância e Input Shaper.

### Utilização

- Medição das ressonâncias
- Calibração do eixo X
- Calibração do eixo Y
- Ajuste do Input Shaper
- Redução de ringing e ghosting

A configuração pode ser carregada separadamente através de:

```ini
[include ADXL345.cfg]
```

quando necessária para calibração.

---

# 🌡️ Monitoramento

O Klipper monitora diferentes temperaturas da máquina.

### Hotend

Termistor:

`EPCOS 100K B57560G104F`

Temperatura máxima configurada:

**300 °C**

### Mesa

Termistor:

`EPCOS 100K B57560G104F`

Temperatura máxima configurada:

**130 °C**

### MCU

A temperatura da SKR Mini E3 V3 também é monitorada:

```ini
[temperature_sensor MCU]
sensor_type: temperature_mcu
```

### Host Klipper

O computador que executa o Klipper também possui monitoramento:

```ini
[temperature_sensor PC]
sensor_type: temperature_host
```

---

# ❄️ Refrigeração

A impressora possui controle independente para:

- Part Cooling Fan
- Heatbreak Cooling Fan
- Controller Fan

Também foram realizadas modificações físicas de refrigeração, incluindo:

- Ventoinha de **60 × 20 mm** na região da placa-mãe
- Dissipadores nos motores
- Refrigeração modificada da eletrônica
- Ventoinha de **120 mm** na fonte

---

# 🏠 Enclosure

A impressora trabalha dentro de um enclosure.

Isso ajuda principalmente na estabilidade térmica durante a utilização de materiais como ABS.

A temperatura interna pode ficar aproximadamente na faixa de:

**35–37 °C**

dependendo das condições de impressão.

---

# 🧪 Materiais

A máquina é utilizada com diferentes materiais:

- PLA
- PETG
- ABS
- TPU

Cada material possui seu próprio perfil de impressão e calibração.

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

As calibrações podem mudar conforme novos upgrades forem instalados.

---

# 🤖 Recursos e automações

A configuração utiliza recursos do Klipper e Moonraker como:

- Macros personalizadas
- Mainsail
- Moonraker
- Exclude Object
- Timelapse
- Bed Mesh
- Input Shaper
- Pressure Advance
- BTT SFS V2
- Pause / Resume
- Skew Correction
- Force Move
- Monitoramento de temperatura
- Comandos Shell
- Som ao finalizar impressão

---

# 📂 Estrutura do projeto

A ideia é manter todas as configurações da impressora neste mesmo repositório.

```text
Ender-3-V2-Klipper-Modded-OrangeK08/
│
├── README.md
├── LICENSE
│
├── printer.cfg
├── mainsail.cfg
├── macro.cfg
├── timelapse.cfg
├── btt-sfs-v2.cfg
├── shell_command.cfg
│
├── ADXL345.cfg
│
├── calibration/
│   └── resultados de calibração
│
└── images/
    └── fotos da impressora
```

---

# 📄 printer.cfg

O arquivo principal do projeto é:

[`printer.cfg`](./printer.cfg)

Ele contém as principais configurações da máquina, incluindo:

- MCU
- Cinemática cartesiana
- Limites de movimento
- Stepper X
- Stepper Y
- Stepper Z
- TMC2209
- Extrusor
- Hotend
- Mesa aquecida
- Ventoinhas
- CR Touch
- Safe Z Home
- Input Shaper
- Sensores de temperatura
- Board Pins
- Skew Correction

Outros arquivos `.cfg` são carregados pelo `printer.cfg` através de `[include]`.

---

# 🚀 Objetivos do projeto

O projeto busca continuar evoluindo a Ender 3 V2 para alcançar:

- 🚀 Maior velocidade
- ⚡ Maior aceleração
- 🎯 Maior precisão
- 🖨️ Melhor qualidade de impressão
- 📉 Menos ringing e ghosting
- 🔧 Maior confiabilidade mecânica
- 🌡️ Melhor controle térmico
- 🤖 Mais automação
- 📊 Melhor monitoramento
- 🧵 Maior segurança na alimentação do filamento

A máquina continuará recebendo melhorias e novas calibrações.

---

# ⚠️ Aviso importante

**Não copie este `printer.cfg` diretamente para outra impressora sem revisar a configuração.**

Verifique especialmente:

- Placa-mãe
- MCU
- Pinagem
- Drivers
- Corrente dos motores
- Sentido dos motores
- Endstops
- Dimensões dos eixos
- Limites de movimento
- CR Touch / BLTouch
- Z Offset
- Hotend
- Termistores
- PID
- Rotation Distance
- Input Shaper
- Pressure Advance
- Sensores de filamento

Uma configuração incorreta pode provocar movimentos inesperados, colisões ou outros problemas no equipamento.

**Utilize este projeto como referência e calibre sua própria máquina.**

---

# 📜 Licença

Este projeto é distribuído sob a **MIT License**.

Você pode utilizar, modificar e compartilhar o conteúdo conforme os termos da licença.

Consulte:

[`LICENSE`](./LICENSE)

---

# 👤 Autor

**OrangeKnight08 — OrangeK08**

Projeto pessoal de modificação e evolução da **Creality Ender 3 V2**.

⭐ Se este projeto foi útil para sua própria Ender 3 V2, considere deixar uma estrela no repositório.
