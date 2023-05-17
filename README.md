# PARCIAL SPD - AGUSTIN DI LEONE

## Alumno:
- Agustin Di Leone


## Proyecto: Montacarga funcional como maqueta para un hospital.
![Tinkercad](https://github.com/AgustinDiLeone/PARCIAL_SPD/blob/main/Img/Di%20Leone%20-%20PARCIAL.png)


## Descripción
El objetivo es implementar un sistema que pueda recibir ordenes mediante pulsadores de subir, bajar o detener
desde diferentes pisos y muestre el estado actual del montacargas en el display 7 segmentos y mediante el 
monitor Serial.

## Funciónes 
Esta funcion se encarga de encender y apagar los leds.

LED_A, LED_B, LED_C, LED_D, LED_E, LED_F, LED_G son #define que utilizamos para agregar el 7-segmentos,
SUBIR, BAJAR, DETENER son #define que utilizamos para agregar los botones,
ROJO, VERDE son #define que utilizamos para agregar los leds, asociandolo a pines de la placa arduino.

intervalo, estado, contador = 0, piso = 1 los declare como enteros y algunos los inicialice,
tiempo = 0 y tiempo2 = 0, los declare como "unsigned long",
tiempo lo inicialice con la funcion "millis()"

Funcion para que suba, baje o se detenga, mediante un contador:
Enciende o apaga los led segun el estado,
Informa si se llego al piso maximo o minimo,
Comprueba si pasaron los 3 segundos entre piso y piso.

~~~ C (lenguaje en el que esta escrito)

void loop()
{
    tiempo2 = millis();
    if (digitalRead(SUBIR) == LOW)
    {
        encender_led(VERDE);
        apagar_led(ROJO);
        if (tiempo2 > (tiempo + 3000))
            {
                if (contador == 3)
                    {
                        Serial.println("Se ha llegado al piso maximo");
                    }
                else
                {
                    contador ++;
                }
            }
    }
    else if (digitalRead(BAJAR) == LOW)
    {
        encender_led(VERDE);
        apagar_led(ROJO);
        if (tiempo2 > (tiempo + 3000))
            {
                if (contador == 0)
                    {
                        Serial.println("Se ha llegado al piso minimo");
                    }
                else
                {
                    contador --;
                }
            }
    }
    else if (digitalRead(DETENER) == LOW)
    {
        encender_led(ROJO);
        apagar_led(VERDE);
        Serial.println("Se detuvo el montacargas");
    }
    if (contador == 0 && piso != 0)
    {
        mostrar_0();
        Serial.println("Estas en el piso 0");
        tiempo = millis();
        piso = 0;
    }
    else if (contador == 1 && piso != 1)
    {
        mostrar_1();
        Serial.println("Estas en el piso 1");
        tiempo = millis();
        piso = 1;
    }
    else if (contador == 2 && piso != 2)
    {
        mostrar_2();
        Serial.println("Estas en el piso 2");
        tiempo = millis();
        piso = 2;
    }
    else if (contador == 3 && piso != 3)
    {
        mostrar_3();
        Serial.println("Estas en el piso 3");
        tiempo = millis();
        piso = 3;
    }
}
~~~

Funcion para encender led que se ingresa por parametro:

~~~ C (lenguaje en el que esta escrito)
void encender_led(int led)
{
	digitalWrite(led,HIGH);
}
~~~

Funcion para apagar led que se ingresa por parametro:

~~~ C (lenguaje en el que esta escrito)
void apagar_led(int led)
{
	digitalWrite(led,LOW);
}
~~~
Funciones para mostrar un numero deseado en el 7-segmentos:

~~~ C (lenguaje en el que esta escrito)
void apagar_screen() 
{
    apagar_led(LED_A);
    apagar_led(LED_B);
    apagar_led(LED_C);
    apagar_led(LED_D);
    apagar_led(LED_E);
    apagar_led(LED_F);
    apagar_led(LED_G);
}
void mostrar_0()
{
    encender_led(LED_A);
    encender_led(LED_B);
    encender_led(LED_C);
    encender_led(LED_D);
    encender_led(LED_E);
    encender_led(LED_F);
    apagar_led(LED_G);

}
void mostrar_1()
{
    apagar_led(LED_A);
    encender_led(LED_B);
    encender_led(LED_C);
    apagar_led(LED_D);
    apagar_led(LED_E);
    apagar_led(LED_F);
    apagar_led(LED_G);

}
void mostrar_2()
{
    encender_led(LED_A);
    encender_led(LED_B);
    apagar_led(LED_C);
    encender_led(LED_D);
    encender_led(LED_E);
    apagar_led(LED_F);
    encender_led(LED_G);

}
void mostrar_3()
{
    encender_led(LED_A);
    encender_led(LED_B);
    encender_led(LED_C);
    encender_led(LED_D);
    apagar_led(LED_E);
    apagar_led(LED_F);
    encender_led(LED_G);
    
}
~~~
## Montacargas: Diagrama esquematico del circuito
("C:\Users\beatr\OneDrive\Escritorio\Carpetas GitHub\PARCIAL_SPD\Img\Di Leone - PARCIAL.pdf")

## Montacargas: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/ioNYFIwpfZo-di-leone-parcial/editel?sharecode=_cKTnzVTTVZnBbaxy1mXyRSWi7BOkBeHBpj7odi3OjM)
