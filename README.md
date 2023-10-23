# Primera parte del parcial domiciliario

## Integrantes
- Ignacio Cruz
* Juan Espadero
+ Rocio Natali De Grazia

## Proyecto: Contador de 0 a 99 con display de 7 segmentos y multiplexación.

![arduinoparte1](https://github.com/rrociodg/Parte-1-SPD-/assets/139300487/8a63f921-4d1e-4ce3-b3dd-49bccc802d0e)

## Descripción

El proyecto presentado en esta parte implementa un contador de 0 a 99 utilizando dos leds de 7 segmentos y tres pulsadores para controlar la cuenta, donde uno incrementa su valor, el otro hace que disminuya y por ultimo uno que reinicie el mismo.  La propuesta ofrece una solución para crear un contador numérico simple con dos dígitos que es de control y visualización sencilla. Se utiliza la técnica de multiplexación para mostar los dígitos en los displays. En el siguiente apartado mostraremos una descripción detallada del código en donde se muestran todas las funciones del mismo. 

## Función principal 

Comenzamos definiendo las variables de las constantes para representar los pines y valores utilizados en el proyecto. 
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

# Segunda parte del parcial domiciliario

## Proyecto: Modificación con Interruptor Deslizante y Números Primos

![arduinoparte2](https://github.com/rrociodg/PARCIAL-SPD/assets/139300487/116bce8d-3d9d-4d7a-8227-97bcec98c7ec)

## Descripción
En esta parte del proyecto se utiliza el mismo contador que va de 0 a 99 con 2 display de 7 segmentos pero se agrega un sistema de control de temperatura, un motor de CC (corriente continua) y una opcion para visualizar los numeros primos. La opcion de contador o numeros primos esta determinada por un interruptor. En el caso de posicionarse en la parte de contador el sistema ademas de mostrar el cronometro, monitorea la temperatura a través de un sensor y enciende el motor si la temperatura está dentro de un rango deseado para mantenerla en un nivel óptimo. Si se selecciona la opción de numeros primos, se muestran los numeros correspondientes en los displays, y según que boton se presione, o aumenta el numero o lo desciende. Si se llega al limite el mismo se reinicia. 

## Funcion principal 

El comienzo de este proyecto es muy similar al presentado en la parte 1. Se comienza el codigo definiendo las constantes que representan numeros de pin y valores. Nos ayudan a organizar nuestro proyecto. 

Se sigue con la  configuracion inicial del proyecto definido en el
~~~ C
void setup()
~~~
Aquí se están configurando varios pines, tanto como entradas como salidas, y se inicia la comunicación serial.
~~~ C
"pinMode()
Serial.begin()
digitalWrite()"
~~~
- Se configuran los pines A, B, C, D, E, F y G, como salidas digitales. 
- Se configuran varios pines como entradas con resistencias pull-up internas habilitadas( interruptor: Un pin que se usa para leer el estado de un interruptor o botón, UPbttn: Un pin que se utiliza para leer si se presiona un botón de aumento y DOWNbttn: Un pin que se utiliza para leer si se presiona un botón de disminución )
- Se configura el pin motor como una salida digital.
- Se configuran los pines UNIDAD y DECENA como salidas digitales.
- Los pines UNIDAD y DECENA se establecen en un estado LOW al inicio, es decir que esten, apagados
- Por ultimo, se inicia la comunicacion que permite la depuración para ver información a través del puerto serie.

Finalmente se inicializan varias variables, las cuales se utilizan para rastrear el estado de los botones, controlar el funcionamiento del contador y gestionar la medición de la temperatura y otros sensores en el proyecto. Cada una tiene un propósito específico en el funcionamiento general del programa.

~~~ C
int countDigit = 0;    //registro del contador
int sube = 1;		  //rastrear el estado del boton de aumento.
int baja = 1;		 // rastrear el estado del boton de disminución.
int subePrevia = 1; // Ayudan a detectar cuándo se presionan o sueltan los botones.
int bajaPrevia = 1;//  registro del estado anterior de los botones 
bool numeroPrimo; //   determina si un numero es primo o no 
int countP = 2;  // Se muestra los numeros primos 
int lectura = 0;// Almacena la lectura analógica del sensor
float temperatura = 0;
~~~

Una vez terminado se continua con la funcion
~~~ C
void prenderLed(int led)
~~~
La cual funciona exactamente que la parte anterior, en donde la tarea especifica de la funcion es encender el led o segmento especificado. 

~~~ C
int keypressed(void)
~~~
Es la que realiza la detección de si los botones fueron o no presionados, y en caso de que si, devuelve cual ha sido. Para evitar que  se repita, compara el estado actual con el previo. Si no se presiona ninguno devuelve 0.

~~~ C
bool esPrimo(int n)
~~~
Lo que esta funcion hace es chequear si un numero es o no primo. Comienza comprobando si el numero es menor o igual a 1, si es asi devuelve “False” , ya que los numeros primos son positivos. Luego, se realiza la verificacion si el numero “n” es divisible por algun numero entre 2 y la raiz cuadrada de “n”. Si se encuentra un divisor, devuelve “False”, caso contrario, devuelve “True” indicando que el mismo es numero primo. 

Se continua con la funcion 
~~~ C
void printCount(int count)
~~~
Se encarga de dividir un número en sus partes de decenas y unidades, y luego muestra esas partes en un display de siete segmentos secuencialmente. Esto permite mostrar números de dos dígitos en el display.

~~~ C
void printDigit(int digit)
~~~
Esta funcion prepara a los leds en estado apago y según el numero que corresponda se activan los leds correspondientes. Este proceso se realiza a través de una estructura llamad switch. Esta función es esencial para la representación de dígitos en el display de siete segmentos y se utiliza en combinación con la función prenderLed para mostrar números en el proyecto.

~~~ C
int siguientePrimo(int n)
int anteriorPrimo(int n)
~~~
En la primera funcion como el nombre lo describe se trata de buscar el siguiente numero primo al que se muestra por display, se utiliza la logica en donde  a partir del número n, aumenta el valor de n en uno y luego entra en un bucle while. En cada iteración se reutiliza la función "esPrimo()". Si es primo, devuelve ese número como el siguiente primo mayor. Si no, lo continua buscando. En la otra funcion, en lugar de aumentar lo disminuye y se asegura que no sea menor a 2 ya que dicho numero es el numero primo más pequeño. 

Al igual que en la parte 1 se volvio a reutilizar la funcion en donde se verifica si se debe mostrar el dígito en el display de unidades (UNIDAD) o en el display de decenas (DECENA).
~~~ C
void prendeDigito(int digito)
~~~

Ya adentrandonos en el final del proyecto se inicializa 
~~~ C
void loop()
~~~
Que como ya dijimos es el encargado de ejecutar continuamente nuestro programa hasta que el mismo finalice. El mismo consta de varias partes:
~~~ C
int pressed = keypressed()
para saber si fueron los botones presionados
~~~

~~~ C
int modo = digitalRead(interruptor)
lee el estado del interrumptor para saber en que modo operar.
~~~
Si el interruptor se encuentra en el modo 1 significa que el proyecto esta en modo de control de temperturas, y va a verirficar el estado de la misma. En el caso de que la temperatura no sea optima el motor se apaga. La temperatura  es leida en un valor analogico del sensor de temperatura(sensortmp), y el codigo  mapea este valor en el rango entre 0 y 1023 a un rango de -50°C a 450°C, y luego lo divide por 100 para obtener la temperatura en grados Celsius y la almacena en la variable "temperatura". Si al contrario, el interruptor esta en modo 0, significa que el proyecto esta en numeros primos. Si se presiona el boton para incrementar el numero aumenta tratando de no superar el 97, si se presiona al contrario el que disminuye, decrece su valor teniendo como limite el 0, para que los numeros aparezcan por los display se llama a la funcion “printCount()” para mostrar el valor actual. 

## :question: Explicación de la elección del motor CC y el sensor de temperatura
El motor de corriente continua es un dispositivo con la capacidad de convertir energía eléctrica en trabajo mecánico a través de fuerzas electromagnéticas. Estos motores son ampliamente utilizados en aplicaciones donde se necesita un control preciso de la velocidad y puede ser aprovechado en objetos que requieran movimiento, tales como aparatos de uso cotidiano como juguetes y electrodomésticos, pero también en maquinaria industrial en menor escala. Lo elegimos para nuestro proyecto ya que los motores de CC son conocidos por su eficiencia energética, lo que significa que pueden realizar tareas mecánicas con menor consumo de energía en comparación con algunos motores de aficionado, y además pueden ser más versátiles en términos de diseño y se pueden adaptar a diferentes aplicaciones. El sensor de temperatura lo consideramos una elección sumamente importante ya que permite monitorear la temperatura constantemente, inclusive lo hace más seguro, ya que si supera la tempertura ideal el mismo se detiene para evitar daños.

# Tercera parte del parcial domiciliario(Fotodiodo-Fototransistor)
* Fotodiodo
![arduinoparte3](https://github.com/rrociodg/PARCIAL-SPD/assets/139300487/31d09d0e-4664-47bf-8dda-8c1079964559)
* Fototransistor
![arduinoparte3fototransitor](https://github.com/rrociodg/PARCIAL-SPD/assets/139300487/58ad46a5-ca35-4489-899f-68e8904ccb1f)

## Funcion del fotodiodo
Un fotodiodo es un dispositivo semiconductor que, en términos sencillos, es como un pequeño sensor de luz. Está diseñado para convertir la luz en electricidad. Funciona en base al principio del "efecto fotovoltaico", lo que significa que cuando la luz incide sobre él, genera electricidad. El fotodiodo, en este proyecto, se utiliza para medir la intensidad de la luz en el entorno. El valor leído por el fotodiodo se convierte en una señal eléctrica que se puede usar para diferentes decisiones. La lectura de la intensidad de la luz mediante el fotodiodo se realiza de la siguiente manera:
~~~ C
int lecturaFotodiodo = analogRead(sensor);
~~~
Luego toma decisiones segun el valor indicado, dependiendo la intensidad de la luz, realizara diferentes acciones.
~~~ C
   
    if (lecturaFotodiodo > 800) {
      analogWrite(motor, 1);  // disminuir la velocidad del motor.
    } else if (lecturaFotodiodo < 200) {
      analogWrite(motor, 220);  // aumentar la velocidad del motor.
    } else {
      analogWrite(motor, 127);  //velocidad intermedia.
    }
~~~

## Funcion del fototransistor

El fototransistor agregado a la parte tres, es un semiconductor donde su funcion es detectar la intensidad de luz ambiental. Por su nombre similiar al de un transistor a diferencia de este se controla por la luz ingresada al sensor.

## :computer: Link a las partes del proyecto
- [PARTE1](https://www.tinkercad.com/things/lmmY99UTZsH-parte1-parcial-/editel)
- [PARTE2](https://www.tinkercad.com/things/2dnIPh4puuS-parte2-parcial-/editel)
- [PARTE3-FOTODIODO](https://www.tinkercad.com/things/l478FNkO91X-parte3-fotodiodo/editelsharecode=1HDkmttMVKUtayZpagTi39exdRXy2OaSJeZjw96aE8Q)
- [PARTE3-FOTOTRANSISTOR](https://www.tinkercad.com/things/4VnTgtksKmE-copy-of-copy-of-copy-of-parte-1-spd/editel?sharecode=3ksGDfHUcPz2qOsi7KTN2c4CyMPwowokdw0__vIMKR4)
  
## :space_invader: Fuentes

- [Como documentar en Github](https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Motor de CC](https://sdindustrial.com.mx/blog/motor-de-corriente-continua/)
- [Sensor luz ambiental](https://www.youtube.com/watch?v=kv6r6HzJDqw)
- [Sensor de temperatura TMP36](https://www.youtube.com/watch?v=jq7vRrz2PKA)
- [Control del motor CC](https://youtube.com/watch?v=fJKPeiwi0Pc)
- [¿Que es un fotodiodo?](https://unicrom.com/fotodiodo/)


