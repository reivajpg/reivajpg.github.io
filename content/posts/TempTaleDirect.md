---
title: "Reutilizacion de TempTale Ultra"
Author: ReivaJPG
date: 2025-02-22
categories: ["mod", "Teardown", "flash", "ARM", "STM32"]
featured: true
---
##Que es TempTales
TempTale es una línea de monitores de temperatura muy prácticos. Deja uno donde sea sensible justo antes del envío de un producto critico y el destinatario puede  verificar rápidamente que la temperatura del paquete se mantuvo durante todo el envío. Abriendo un archivo PDF generado automáticamente en el dispositivo.
El dispositivo aparece como un dispositivo de almacenamiento masivo USB con un archivo PDF  a bordo.




##Desarmando el TempTales
Como funciona 
Internamente, consta de un microcontrolador STM32 ARM, una memoria flash serial externa, una batería de botón con terminales de soldadura, algunos botones, un oscilador de alta y baja velocidad y un panel LCD desnudo.

La pantalla LCD está limpia, ya que la descarga estática en mis dedos provocó un destello de píxeles cuando la toqué por primera vez. Además, preste atención al borde frontal que se encuentra debajo: el vidrio tiene contactos de metal que luego tocan láminas de metal delgadas incrustadas en la tira de espuma blanca gruesa en la parte frontal. El contacto se mantiene en su lugar mediante la carcasa y la placa de circuito impreso.


En cuanto al software, solo se necesitan unos pocos componentes para algo como esto. [Un controlador de almacenamiento masivo USB](http://www.keil.com/download/docs/362.asp) , [un controlador de sistema de archivos](http://www.st.com/content/ccc/resource/technical/document/user_manual/61/79/2b/96/c8/b4/48/19/DM00105259.pdf/files/DM00105259.pdf/jcr:content/translations/en.DM00105259.pdf) , [un escritor de PDF](https://github.com/libharu/libharu/) y algo de lógica personalizada para despertar la CPU de un evento de bajo consumo, probablemente la alarma RTC, leer la temperatura y almacenarla en un búfer circular. Justo antes de la enumeración USB, escriba el búfer circular en un archivo PDF. Los posibles componentes de ejemplo se encuentran en los enlaces anteriores.

Son dispositivos muy prácticos y espero que en el futuro se utilicen más para la validación de envíos. Sensitech incluso fabrica modelos con GPS y acelerómetros.
