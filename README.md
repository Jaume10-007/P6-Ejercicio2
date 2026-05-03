# 📘 Práctica 6 - SPI  
## Ejercicio 2: Escritura y lectura en tarjeta RFID

---

## 🧠 Descripción

En este ejercicio se implementa la comunicación SPI entre un **ESP32-S3** y un **lector RFID RC522** para realizar operaciones de escritura y lectura sobre la memoria de una tarjeta RFID.

El sistema permite:
- Detectar una tarjeta RFID.
- Autenticar un bloque de memoria.
- Escribir un mensaje en la tarjeta.
- Leer el mensaje almacenado.
- Verificar la correcta transmisión de datos.

---

## 🎯 Objetivos

- Comprender el uso del bus **SPI** en sistemas embebidos.
- Implementar escritura de datos en una tarjeta RFID.
- Leer información previamente almacenada.
- Trabajar con memoria estructurada en bloques.
- Introducir conceptos de autenticación en RFID.

---

## 🔌 Hardware utilizado

- ESP32-S3  
- Módulo RFID RC522  
- Tarjeta RFID MIFARE Classic  
- Llavero RFID  

---

## ⚙️ Conexiones

| RC522        | ESP32-S3 |
|-------------|----------|
| SDA (SS)    | GPIO 10  |
| SCK         | GPIO 12  |
| MOSI        | GPIO 11  |
| MISO        | GPIO 13  |
| RST         | GPIO 9   |
| VCC         | 3.3V     |
| GND         | GND      |

---

## 🚀 Funcionamiento del programa

1. Inicializa la comunicación serie.
2. Inicializa el bus SPI.
3. Inicializa el módulo RC522.
4. Configura la clave por defecto de autenticación (`FF FF FF FF FF FF`).
5. Espera a detectar una tarjeta RFID.
6. Cuando detecta una tarjeta:
   - Muestra el UID.
   - Identifica el tipo de tarjeta.
   - Autentica el bloque de memoria seleccionado.
   - Escribe un mensaje en el bloque.
   - Lee el mismo bloque.
   - Muestra el mensaje almacenado.
7. Finaliza correctamente la comunicación con la tarjeta.

---

## 💾 Escritura en memoria RFID

Se utiliza:

- **Bloque 4** de la tarjeta.
- Tamaño máximo: **16 bytes**.

Mensaje utilizado en el código: VIVA ESPANYA

---

## ⚠️ Importante

- No escribir en bloques **trailer** (3, 7, 11, 15...).
- Solo funciona correctamente con tarjetas **MIFARE Classic**.
- Se utilizan claves por defecto.

---

## 📊 Ejemplo de salida

```text
======================================
 TARJETA DETECTADA
======================================
UID detectado: 43 A2 91 0B
Tipo de tarjeta: MIFARE 1KB
Bloque usado para escritura/lectura: 4

[OK] Autenticacion correcta
[OK] Mensaje escrito correctamente
[OK] Mensaje leido correctamente

Mensaje guardado: VIVA ESPANYA
Datos en HEX: 56 49 56 41 20 45 53 50 41 4E 59 41 20 20 20 20

======================================
 FIN DE OPERACION
======================================
