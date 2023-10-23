# Primera parte del parcial domiciliario

## Integrantes
- Ignacio Cruz
* Juan Espadero
+ Rocio Natali De Grazia

## Proyecto: Contador de 0 a 99 con display de 7 segmentos y multiplexación.

[Tinkercad]![arduinoparte1](https://github.com/rrociodg/Parte-1-SPD-/assets/139300487/8a63f921-4d1e-4ce3-b3dd-49bccc802d0e)

## Descripción

El proyecto presentado en esta parte implementa un contador de 0 a 99 utilizando dos leds de 7 segmentos y tres pulsadores para controlar la cuenta, donde uno incrementa su valor, el otro hace que disminuya y por ultimo uno que reinicie el mismo.  La propuesta ofrece una solución para crear un contador numérico simple con dos dígitos que es de control y visualización sencilla. Se utiliza la técnica de multiplexación para mostar los dígitos en los displays. En el siguiente apartado mostraremos una descripción detallada del código en donde se muestran todas las funciones del mismo. 

## Función principal 

Comenzamos definiendo las variables de las constantes para representan los pines y valores utilizados en el proyecto. 
~~~ C
void setup()
~~~
Se inicia la funcion setup(). En dicha parte, se están configurando varios pines como salidas (OUTPUT) o entradas con resistencias pull-up internas habilitadas (INPUT_PULLUP), y se inicia la comunicación serial, es decir, le indicamos a la placa de Arduino cómo debe funcionar y qué pines usaremos para el funcionamiento del contador de 0 a 99 con displays de 7 segmentos y botones. Se ejecuta una sola vez al principio del programa. 

Se procede iniciando las variables que se van a utilizar para rastrear las acciones del usuario y el estado del programa a medida que se ejecuta. Dependiendo el boton que por ejemplo toque hace cierta acción.

~~~ C
void prenderLed(int led)
~~~
En esta funcion presentada se toma un parametro llamado “led” que representa el pin al que está conectado el LED o segmento que se desea encender. Cuando se llame a esta funcion y se le pase un numero de pin se enciende el led o segmento conectado configurandolo en estado HIGH y esta asociada directamente con la funcion siguiente
~~~ C 
“void prenderNumero”,
~~~
la cual  se encarga de encender los segmentos correspondientes para representar desde el numero 0 al 9.

~~~ C
int keypressed(void)
~~~
Detecta si se ha presionado alguno de los botones: "subir", "bajar" o "restablecer". Devuelve el botón presionado como resultado. Para hacerlo, compara el estado actual de los botones con su estado previo y devuelve el botón si ha cambiado de estado. Si ningún botón se ha presionado, devuelve 0.

~~~ C
void prendeDigito(int digito)
~~~
La funcion toma un parametro llamado “digito” que generalmente representa si se debe mostrar el dígito en el display de unidades  o en el display de decenas. La funcion realiza lo siguiente:
* DIGITO =  UNIDAD: enciende el display de unidades y apaga el de decenas. Se espera un breve momento de tiempo definido por + TIMEDISPLAYON.
- DIGITO = DECENA: enciende el display de decenas y apaga el de unidades. Tambien espera un momento de tiempo definido por TIMEDISPLAYON
* Si DIGITO no es representando por ninguno de los dos, se mantiene los displays apagados. 

~~~ C
void loop()
~~~
Esta es la función principal que se ejecuta de manera constante hasta que el programa se pare. En ella, se controla un contador que puede aumentar, disminuir y restablecer su valor según lo que el usuario presione. Luego, muestra el valor actual del contador en los displays de 7 segmentos

~~~ C
void printCount(int count)
~~~
Es la encargada de mostrar un número de dos dígitos en los displays de 7 segmentos, dividiendo y mostrando el dígito de las decenas y unidades de manera independiente.

Para finalizar el programa se utiliza la función:

~~~ C
void printDigit(int digit)
~~~
La misma se utiliza para mostrar un numero especifico en los display. La funcion inicialmente los apaga a todos los segmentos  para luego utilizar un “switch” para determinar que segmentos deben encenderse para mostrar el numero correcto. Cada caso corresponde a un numero de 0 al 9. 

## :computer: Link al proyecto.
- [proyecto](https://www.tinkercad.com/things/lmmY99UTZsH-parte1-parcial-/editel)

## :space_invader: Fuentes

- [Como documentar en Github](https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)


