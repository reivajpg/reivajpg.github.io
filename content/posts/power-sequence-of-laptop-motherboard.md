---
title: "Secuencia de arranque de la placa base de un laptop"
date: 2023-05-31T10:00:00Z
image: /images/post/post-2.png
categories: ["laptop","motherboard","repair"]
featured: false
draft: false
---
## Secuencia de arranque de la placa base de un laptop

Comprender la secuencia de potencia de las placas base de las computadoras portátiles es muy importante. En primer lugar, la secuencia de potencia es el intercambio de voltajes y señales entre los chips de la placa base.

En segundo lugar, esto sucede antes de que aparezca algo en la pantalla.

La secuencia de potencia es la fase en la que la placa base se prepara para funcionar. Esta fase consiste en enviar órdenes a diferentes generadores de voltaje desde algunos circuitos integrados. En segundo lugar, recibir la confirmación garantiza que los principales circuitos integrados de la placa base funcionen.

La secuencia de potencia debe tener lugar en un orden específico. En segundo lugar, si no se envía o recibe una señal o confirmación, esta fase se detiene allí y, finalmente, nada funcionará.

La secuencia de potencia se utiliza para [solucionar problemas de la placa base de la computadora portátil](https://displaymonk.com/laptop-chip-level-repair-career-guide/) mediante la prueba de voltajes porque la ausencia de algunos voltajes indica problemas con algunos circuitos integrados. También en algunos esquemas, se describe la secuencia de potencia, lo que facilita la resolución de problemas.


### Pasos para verificar el voltaje y la secuencia de señal para la placa base de la computadora portátil en el escenario
Los escalones se conocen como escaleras para voltajes y señales. Estos pasos se dan a continuación.

1. ALWAYS VOLTAGE Checking:
    Estos voltajes se genera antes de que se presione el botón de encendido. Se proporcionan 3 voltios a SIO y EC BIOS.

2. After Pressing The POWER BUTTON:
    Una vez que el botón de encendido presiona SIO([Super I/O](https://en.wikipedia.org/wiki/Super_I/O)) para informar al PCH y encender los [buck converters](https://en.wikipedia.org/wiki/Buck_converter) uno tras otro.

3. POWER ON VOLTAGES check:
    Los voltajes después del encendido debe producirse como se indica a continuación:
        3.3 Volt
        5 Volt
        1.8 Volt
        1.5 Volt
        1.05 Volt
        CPU CORE
        0.9 GFX Core

4. POWER GOOD Signal Check:
    El PCH recibe la señal de confirmación de la señal SYS PWR OK que dice que toda la energía está bien.

5. RESET Signal Check:
    El PCH genera una señal PLTRST para borrar los valores basura de la placa base y restablecer la placa base.

6. CLOCK SIgnal Check:
    El CLOCK comienza a generar diferentes frecuencias según los requisitos de los chips.

7. Starts Reading BIOS:
    En este paso, la CPU comienza a leer [BIOS](https://en.wikipedia.org/wiki/BIOS) .

8. POST Checking By Motherboard:
    En este paso, la placa base prueba todos los chips y dispositivos en este proceso que también se denomina 'Autocomprobación de encendido'.

##### Estados de energía de la placa base para comprender el poder de la placa base de la computadora portátil en las etapas de secuencia:

Estos son los estados del portátil en función de su consumo de energía, ya conoces dos estados que son:
        Enciendes la Laptop.
        La computadora portátil se apaga por usted.

Los estados de la placa base se mencionan en el carácter 'Sx' donde la x es un número entre 0 y 5.

S0 State:
    Funcionando, el sistema es totalmente utilizable, todos los componentes tienen voltaje.

S1, S2, S3 State:
    Suspender, la computadora portátil parece estar apagada, la computadora portátil consume menos energía que en el estado S0, la RAM tiene su voltaje y se mantiene actualizada. Para despertar la computadora portátil de este estado de suspensión, solo necesita presionar una tecla en el teclado o mover el mouse.

S4 State:
    Hibernate, el sistema parece estar apagado y el consumo de energía se reduce al nivel más bajo. Se mantiene una imagen de la RAM en el disco porque la RAM pierde sus voltajes, para activar la computadora portátil debe presionar el botón de encendido.

S5 State:
    En este estado, la placa base de la computadora portátil se apaga.



### Tipos de voltajes en la placa base para etapas de secuencia de encendido:

Hay cuatro etapas en la placa base de la computadora portátil que se detallan a continuación:

#### Always Supply Voltage Type (ALWS or AUX or AL) / Suministros de voltaje siempre activos (ALWS o AUX o AL):
        Estos voltajes siempre están presentes incluso cuando la computadora portátil está apagada, con una condición: la batería debe estar colocada o el cargador enchufado. Estos voltajes son:

    5 voltios CC
    3,3 voltios CC
Los 5 voltios y los 3,3 voltios provienen de circuitos integrados generadores de voltaje en la placa base .

#### Suspension Voltage Type (SUS ON) / Suministro de voltaje de suspensión (SUS ON)
        Estos voltajes están presentes en modo suspendido o dormido (S1, S2, S3):

    5 voltios CC
    3,3 voltios CC
    Voltaje de RAM (para DDR1: 2,5 voltios, para DDR2: 1,8 voltios, para DDR3: 1,5 voltios, para DDR4: 1,2 voltios)
Tenga en cuenta que el 5 Volt y el 3.3 Volt no son los mismos que los ALWS, hay otros bucks que genera esos 5 voltios y 3.3 Volt.

#### Power On Voltage Type (RUN) (S0 State)
        Todos los componentes tienen ahora sus voltajes. Hay un suministro de 1,05 voltios y también se hace 1,8 voltios.

#### CPU Core Voltage Type / Tipo de voltaje del núcleo de la CPU
        La CPU requiere voltaje central, por ejemplo, una corriente alta de aproximadamente 20 amperios a 30 amperios. El chip de gráficos de la placa base más nuevo también está integrado en la CPU. Por lo tanto, también se requiere el voltaje del núcleo de gráficos. Estos voltajes son voltajes de núcleo GFX. Estos voltajes son aproximados:

    CPU Core = 0,8 voltios a 1,5 voltios / 20 amperios a 30 amperios.

    GFX Core = 0,8 voltios a 1,5 voltios / 10 amperios a 20 amperios.


#### Voltages de entrada de la placa base del ordenador portátil
        Hay dos fuentes de entrada de energía en la placa base de una computadora portátil, una es la entrada del adaptador y otra es la entrada de la batería.

La entrada del adaptador y la sección de carga de la batería se denominan secciones VIN (Voltage Injection). Esta sección decide qué energía debe enviarse al interior. Esta sección tiene otra tarea que es la carga de batería(Battery Charging) donde se utilizan varios buck converters para cumplir con esta tarea.



### List Of Laptop Motherboard Power On Signals
The following are laptop motherboard power on signals:

| SIGNAL NAME        | DESCRIPTION                                                                |
|--------------------|----------------------------------------------------------------------------|
| VCC                | 3 Volt power to SIO and BIOS                                               |
| ECRST              | RESET to SIO                                                               |
| LID SWITCH         | The lid sensor should work                                                 |
| THERMTRIP          | The thermal trip should normal                                             |
| Clock SIO          | 32.7khz clock from either PCH                                              |
| EC BIOS            | EC BIOS should perfect                                                     |
| RTCRST             | RTC RESET and crystal 32khz should to PCH                                  |
| VCCDSW3_3          | Power to PCH                                                               |
| DPWROK             | Power OK Indication for the VccDSW3_3 voltage rail                         |
| PWRBTN (NBSON)     | Power switch 3 – 0 – 3 variation                                           |
| RSMRST             | SIO generates 3 Volt at this pin                                           |
| PM_PWRBTN          | Post power button to PCH 3 Volt variation.                                 |
| SLP_4 SLP_3        | PCH generates 3 Volts send to SIO giving confirmation to turn on the power |
| SYSON, SUSP, VR ON | All buck converters turn on one by one                                     | 


### Signal Name And Description For Laptop Power On Signals
When power is connected either from the adapter or battery to the motherboard it passes from various stages.

Below mention a chart given signal name and their description.

| SIGNAL NAME              | DESCRIPTION                                                                                                                   |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| VIN voltage              | Check the input voltage to this current sensing resistor                                                                      |
| VIN                      | VIN is 3 Volt and 5 Volt section input voltage to 3 Volt and 5 Volt chip                                                      |
| VREG3                    | 3 Volt linear output from 3 Volt and 5 Volt section which is going to SIO                                                     |
| VCC                      | SIO gets 3 Volt at its power input pin                                                                                        |
| ECRST                    | EC reset signal 3 Volt reset to SIO                                                                                           |
| THERMTRIP                | THERMTRIP thermal signal                                                                                                      |
| LID SW                   | LID SW is a magnetic lid sensor                                                                                               |
| BIOS                     | EC BIOS starts communicating with SIO                                                                                         |
| NBSWRON /PWRBTN          | The power switch when we press 3 Volt goes zero and then again comes to 3 Volt. Moreover, you can see their 3 Volt variation. |
| ECON                     | SIO generates an ECON signal and turns on always section 3.3 Volt and 5 Volt buck converter output.                           |
| 3.3 Volt ALW, 5 Volt ALW | 3.3 Volt and 5 Volt Buck converter output voltage.                                                                            |
| PCH_PWR EN               | SIO generates this signal and provides power to PCH                                                                           |
| VCCDSW3.3                | PCH power management section gets 3 Volt power                                                                                |
| DPWROK                   | This signal is confirmation to PCH power 3 Volt                                                                               |
| RTCRST                   | RTC reset signal 3 Volt                                                                                                       |
| SUSCLK                   | 32.7KHZ clock frequency to SIO                                                                                                |
| RSMRST                   | SIO sends a 3 Volt signal to PCH to reset and resume called RSMRST                                                            |
| DNBWORON PMBTN           | SIO sends post power button signal to PCH 3 Volt to zero and back                                                             |
| SLP_S4 (SUSB)            | 3 Volt power plane wake up signal to PCH to reset and resume called RSMRST                                                    |
| SPL_S3 (SUSC)            | 3 Volt power plan wake up signal from PCH to SIO                                                                              |
| SYSON, SUSP, VR ON       | SIO turn on all buck converter one by one                                                                                     |




### Diagrama de secuencia de encendido para señales de encendido de portátiles / Power On Sequence Diagram For Laptop Power On Signals
A continuación se muestran los diagramas para las señales de encendido de la computadora portátil.
![alter-text](/images/post/post-1.png)
*Diagrama de secuencia de encendido*


### Señales de encendido de portátiles para placas base generales / Laptop Power On Signals For General Motherboards
A continuación se muestran las señales de encendido para placas base generales. / Below is the power on signals for general Motherboards.


| SIGNAL NAME              | DESCRIPTION                                                                                                         |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| CURRENT SENSING RESISTOR | Check here 18 Volt. Secondly, if not coming then check 1st or 2nd MOSFET or battery charging chip                   |
| VIN                      | DC Voltage input to always voltage chips at its VIN pin                                                             |
| VREG3                    | 3 Volt linear output from the chip                                                                                  |
| VCC                      | 3 Volt power to SIO and BIOS                                                                                        |
| ECRST                    | 3 Volt reset signal to SIO                                                                                          |
| AC OK                    | 3 Volt signal coming from battery charging chip indicating power coming from adapter.                               |
|                          | SIO start communicating with BIOS                                                                                   |
| NBSWRON                  | The power switch goes zero and comes back to 3 Volt                                                                 |
| S5_ENABLE                | After the power button is pressed SIO generates an S5_ENABLE signal to 3 Volt and turns on the 3 and 5 Volt section |
| VCCDSW3_3                | This 3 Volt power turn on PCH                                                                                       |
| DPWROK                   | Power ok to PCH 3 Volt                                                                                              |
| SUSCLK                   | 32.7KHZ clock frequency coming from PCH to SIO                                                                      |
| RSMRST                   | Resume Reset Signal                                                                                                 |
| DNBWRON PM_PWRON         | Post power button signal generate from SIO to PCH                                                                   |
| SLP_3 SLP_4              | Wake up signal generated by PCH send to SIO                                                                         |
| SUS ON SYSON             | Buck converter on signal                                                                                            |



 


![Fuente](https://displaymonk.com/power-sequence-of-laptop-motherboard/)
[Fuente Intel](https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/ia-adv-board-bring-up-paper.pdf)
