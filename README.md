# Practica-ESP32-LCD-ULTRASONICO-y-DH22

En este repositorio se mostrara como programar un ESP32 con un sensor ULTRASONICO y un DH22, con el cual obtendremos las la magnitud de la distancia y algunos datos adicionales se mostraran en una pantalla LCD.

## Introducción 

La placa ESP32 la empleamos para adquirir los datos del sensor ultrasonico. 

La pantalla LCD se empleara para mostrar los datos solicitados:
- Nombre del diplomado
- Nombre
- Carrera profesional
- Fecha
- Distancia (determinada por el sensor ultrasonico)

Esta practica se realizo empleando un simulador: [WOKWI](www.wokwi.com) la cual nos permite simular los elementos y el codigo.

# Material necesario

Para realizar esta practica se necesito
- [WOKWI](www.wokwi.com)
- Una tarjeta ESP32 (para adquisicion de datos)
- Sensor ultrasonico "HC-SR04 Ultrasonic Distance Sensor"
- LCD 16x2 (I2C)

# Instrucciones
1. Abrir la terminal del codigo:

Codigo empleado:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(2000);          //Hacemos una pausa de 100ms

  Serial.println("Distancia: " + String(d) + "cm");
  Serial.println("---");
  
  //Mostrar Diplomado (fila 1); mostrar Automatizacion (fila 2)
  lcd.setCursor(0, 0);
  lcd.print("   Diplomado    ");
  lcd.setCursor(0, 1);
  lcd.print(" Automatizacion ");
  delay(2000);
  lcd.clear();

  //Mostrar nombre (fila 1); mostrar carrera (fila 2)
  lcd.setCursor(0, 0);
  lcd.print(" Hector Vega R. ");
  lcd.setCursor(0, 1);
  lcd.print(" Ing. Mecanica  ");
  
  delay(2000);
  lcd.clear();

  //Mostrar fecha (fila 1)
  lcd.setCursor(0, 0);
  lcd.print("07 de Junio 2025");
  lcd.setCursor(0, 1);
  lcd.print(" ");
  delay(2000);
  lcd.clear();

  //Mostrar la distancia en "cm"
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  lcd.print(" ");
  delay(2000);
  lcd.clear(); 
}

```

2. Instalar la libreria de DHT sensor library for ESPx y en la siguiente imagen se muestran las librerias empleadas.

![](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/librerias.png?raw=true)

3. Hacer las concexiones del sensor ultrasonico HC-SR04 y la pantalla LCD con el ESP32  tal cual se muestra la siguiente imagen.

![](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/conexiones.png?raw=true)

## Librerias empleadas
1. DHT sensor library for ESPx
2. LiquidCrystal I2C

# Intrucciones de operación

1. Iniciar la simulación.
2. Observar los datos del monitor serial.
3. Colorar la distancia simulada haciendo doble click en el Sensor ultrasonico HC-SR04

4. Observar los datos mostrados en la pantalla LCD

# Resultados

Una vez realizados los pasos anteriores deberas visualizar los elementos solicitados en la pantalla LCD

## Pantalla 1:

![](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/diplomado.png?raw=true)

## Pantalla 2:

![](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/nombre%20%20y%20carrera.png?raw=true)

## Pantalla 3:

![image](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/fecha.png?raw=true)

## Pantalla 4:

![image](https://github.com/HV202506/Practica-ESP32-LCD-y-ULTRASONICO/blob/main/distancia.png?raw=true)


# Créditos

Desarrollado por: Ing. Héctor Angel Vega Rodríguez
