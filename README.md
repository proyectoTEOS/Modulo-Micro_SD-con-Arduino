# Modulo Micro_SD con Arduino
Guardaremos datos en un archivo desde una memoria micro-sd con Arduino.

### Requisitos
- Tener el IDE de [Arduino](https://www.arduino.cc/en/Main/Software) (o el de tu preferencia) con la versión más actual
- Contar con la librería [SD](https://github.com/arduino-libraries/SD)
- Tener el material para hacer el proyecto

### Código
**[Aqui](https://github.com/proyectoTEOS/Modulo-Micro_SD-con-Arduino/blob/master/Modulo-Micro_SD-con-Arduino.ino)** podrás obtener el link del código, también dejaremos
una vista previa aquí abajo.

```c++
/*
  Created by TEOS
  Domotic with Arduino https://goo.gl/btZpjs
  YouTube https://goo.gl/k7TUSZ
  Instagram https://goo.gl/zEIjia
  Facebook https://goo.gl/eivraR
  Twitter https://goo.gl/du5Wgn
  Github https://goo.gl/Xl5IiS
  WEB https://www.proyecto-teos.com
*/

#include <SD.h> //https://github.com/arduino-libraries/SD

const String fileNameT = "datalogT.txt";
bool rowTitleT = true;
String serialPrintT;

File dataFileT;

void setup() {
  Serial.begin(9600);
  Serial.print(F("Estado del modulo: "));
  if (!SD.begin(9)) {
    Serial.println(F("No ha sido posible inicar el modulo."));
    return;
  }
  Serial.println(F("Inicio correctamente."));
  if (!SD.exists(fileNameT))
    Serial.println(F("No existe el archivo, pero se creara uno."));
}

void loop() {
  dataFileT = SD.open(fileNameT, FILE_WRITE);
  if (dataFileT) {
    if (rowTitleT) {
      dataFileT.print("sensor1,");
      dataFileT.print("sensor2,");
      dataFileT.println("sensor3");
      Serial.println("Titulo de fila escrito.");
    }
    dataFileT.println(filePrintT());
    dataFileT.close();
    Serial.println("Valores escritos: " + serialPrintT);
  }
  else
    Serial.println("Error al abrir el archivo");
  delay(5000);
}

String filePrintT() {
  rowTitleT = false;
  uint8_t sensor1T = random(10, 25), sensor2T = random(26, 50), sensor3T = random(51, 100);
  serialPrintT = String(sensor1T) + "," + String(sensor2T) + "," + String(sensor3T);
  return  serialPrintT;
}
```

### Diagrama
El siguiente esquemático muestra como se debe conectar todos los componentes con la placa.
![](https://github.com/proyectoTEOS/Modulo-Micro_SD-con-Arduino/blob/master/modulo-micro_sd-con-arduino-5.jpg)
