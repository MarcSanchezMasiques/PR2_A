# Pr2A: Procedimiento

Para empezar el preceso utilizamos el la siguiente funcion: ```attachInterrupt(GPIOPin, ISR, Mode);``` para iniciar una interrupción en base a pin entre pin. Lo hacemos dentro del siguiente void:
```
void setup() {
Serial.begin(9600);
pinMode(button1.PIN, INPUT_PULLUP);
attachInterrupt(button1.PIN, isr, FALLING);
}
```
Las siguientes funciones se utilizan para:

- ```button1.PIN``` estamos estableciendo que puerto GPIO usaremos como una clavija de
interrupción.

- ```FALLING``` se utiliza para que se interrupma cuando el pin va de ```HIGH``` a ```LOW```.

-  ```isr``` se utiliza para llamar al servicio para interrumpir, el codigo es el siguiente:
```
void IRAM_ATTR isr() {
button1.numberKeyPresses += 1;
button1.pressed = true;
}
```
Despues de estos pasos, añadiremos un bucle en el codigo para que cada vez que se pulse el botón 1 muestre por pantalla "Button 1 has been pressed ```%u times\n"``` teniendo en cuenta que ```%u ```es el numero de veces que se ha pulsado el boton. Para completar el bucle añadimos lo siguiente:
```
static uint32_t lastMillis = 0;
if (millis() - lastMillis > 60000) {
lastMillis = millis();
detachInterrupt(button1.PIN);
Serial.println("Interrupt Detached!");
}
```
Este lo que hara es al pasar 1 minuto, automaticamente desconectara la interrupción del pin GPIO que tengamos asignado.
