# Pràctica 8

## Practica 8A: 

Aquest codi implementa un programa de bucle de retorn (loopback) utilitzant un segon port sèrie (Serial2) en un microcontrolador compatible amb Arduino, com l'ESP32

### Objectiu

L'objectiu és enviar dades des de Serial a Serial2 i viceversa, mostrant indicadors per al trànsit de dades.

### Codi

```cpp
#include <Arduino.h> 

#define RXD2 18  //pin 18 com RX (recepció) per al port Serial2
#define TXD2 17  //pin 17 com TX (transmissió) per al port Serial2

//inicialitzacions
void setup() {
  Serial.begin(115200);  
  Serial2.begin(115200, SERIAL_8N1, RXD2, TXD2); 
  delay(1000);  //espera 1 segon per assegurar-se que la comunicació sèrie s'estableix correctament
  Serial.println("Loopback program started");  //missatge per indicar que el programa de bucle de retorn ha començat
}

void loop() {
  if (Serial.available()) {  //Comprova si hi ha dades disponibles per llegir des del port sèrie principal
    Serial.write("-");  //escriu un indicador '-' per mostrar que s'estan enviant dades des del port sèrie principal
    Serial2.write(Serial.read());  //Llegeix una dada del port sèrie principal i l'envia a Serial2
  }
  //igual pero amb el serial2 i "." en comptes de "-"
  if (Serial2.available()) {  
    Serial.write(".");  
    Serial.write(Serial2.read());  
  }
}
```

### Sortida pel port sèrie

Suposem que l'usuari escriu "Hola" al port sèrie principal (Serial). La sortida serà la següent:

Loopback program started
-.-H-.-o-.-l-.-a

### Funcionament del programa
Aquesta implementació permet veure clarament el trànsit de dades entre el port sèrie principal (Serial) i el segon port sèrie (Serial2), demostrant el funcionament del bucle de retorn.
