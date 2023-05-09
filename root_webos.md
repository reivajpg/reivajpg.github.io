Muchos han escuchado cuáles son los derechos de root en Android, pero pocos saben que los derechos de root también se pueden obtener en televisores con webOS. Consulte nuestra guía para aprender a rootear TV desde webOS.

¿Qué son los derechos de raíz?
El término derechos de raíz es uno de los conceptos de Linux, que subyace en el kernel webOS. Root es el nombre de la cuenta de administrador principal, o Superusuario. Al acceder a esta cuenta, automáticamente tiene control total sobre el sistema operativo con la capacidad de personalizar su televisor según sus preferencias. Con la ayuda de los derechos de root, puede, por ejemplo, iniciar automáticamente la aplicación que necesita cuando enciende el televisor.

Precauciones
En caso de problemas con el televisor, el centro de servicio puede rechazar el servicio de garantía. Puede dañar el dispositivo o dejarlo inoperable. Si no es un usuario avanzado y no sabe realmente por qué necesita derechos de root, se recomienda enfáticamente que no los obtenga, porque. siempre existe la posibilidad de obtener un "ladrillo" o cambiar la configuración que causará problemas en el trabajo.

Instrucciones para obtener derechos de root en webOS:
Para trabajar, necesitará: un televisor con webOS conectado a la red, una computadora (conectada a la misma red), una cuenta de desarrollador en el servidor LG.

1. En primer lugar, cree una cuenta de desarrollador (si no está disponible) en el servidor http://developer.lge.com/ ( instrucciones /eng./).
2. Instale la aplicación Developer Mode en el televisor desde el catálogo de aplicaciones de LG Store. Ejecútelo, ingrese el nombre de usuario/contraseña del párrafo anterior, encienda los interruptores Dev Mode Status y Key Server. El televisor se reiniciará y estará listo para más manipulaciones ( instrucción /ing./).
3. Instale el SDK de webOS (solo el componente SDK-CLI) en su computadora desde aquí http://webosv.developer.lge.com/sdk/do ... nload-sdk/ , la forma más fácil es usar el instalador de Internet (" archivo Your_OS_Installer").

http://msx.lh1.in/ipk/


http://webos-forums.ru/post158462.html#p158462
En el firmware más reciente, LG ha bloqueado la capacidad de rootear a través del sitio rootmy.tv, pero hay una nueva forma de obtenerlo:
Nuevas instrucciones abreviadas para rootear televisores LG con webOS 4.x y posteriores usando el exploit crashd:

1. Obtenga el modo desarrollador (modo desarrollador: https://webostv.developer.lge.com/develop/getting-started/preparing-lg-account ), al registrarse, use el correo en la zona .com, por ejemplo, gmail.com. En el televisor de LG Store, instale la aplicación Developer Mode, inicie sesión en su cuenta y active los elementos Dev Mode Status y Key Server .
aplicación-en-modo-desarrollador-de-la-tienda-de-contenido-lg.jpg

2. En el televisor, vaya a Configuración->General->Dispositivos->Control de TV->Quick Boot TV->Apagar;

3. Instale Dev Manager(https://github.com/webosbrew/dev-manager-desktop/releases/) en su computadora y conéctese al televisor ( si no hay conexión al televisor, use la versión 1.7.6 ).
http://webos-forums.ru/download/file.php?id=25081&mode=view/device-manager-for-webos.jpg (Inicie Dev Manager, haga clic en el botón Agregar dispositivo en Opciones. En la ventana que se abre, complete los campos Host (con la dirección IP especificada en el Modo desarrollador en el televisor) y Contraseña (también del televisor). A continuación, haga clic en Agregar.)

4. Instale en TV (a través de Dev Manager) el directorio de la aplicación Homebrew Channel 0.5.1 .

5. Manteniéndote en Dev Manager, haz clic en "terminal" e ingresa el comando en la ventana de la terminal:
CÓDIGO: SELECCIONAR TODO
echo -n > jail_app.conf
Si ocurre un error de Permiso denegado, desconecte el televisor del tomacorriente por un par de minutos, más detalles aquí(http://webos-forums.ru/post163958.html#p163958) .

6. Reinicie su televisor (por ejemplo, apagándolo y encendiéndolo nuevamente). ¡Asegúrese de que Quick Start + (Inicio rápido +) en la configuración del televisor esté deshabilitado!

7. Utilice uno de los dos métodos para obtener la raíz:
Método número 1 . Manteniéndote en Dev Manager, haz clic en "terminal" e ingresa el comando en la ventana de la terminal:
CÓDIGO: SELECCIONAR TODO
touch /var/log/crashd/"x;telnetd -l sh"
y presione Entrar.
Nota: El carácter después del guión es una L minúscula, no una unidad.
Si obtiene el error
sh: touch: not found , simplemente vuelva a intentar el comando. Si tiene éxito, no debería haber ningún resultado.
Método número 2 . Añadir un repositorio alternativo(https://repo.webosapp.club). Ejecute root.telnet desde el repositorio.
http://webos-forums.ru/download/file.php?id=24882&mode=view/webos-homebrew-root-telnet.jpg
Cualquiera de los anteriores ejecutará el exploit "crashd" e iniciará un servidor telnet rooteado en el televisor.

8. Conéctese al televisor a través de Putty (ingrese la dirección IP del televisor en el campo "Nombre de host". Asegúrese de que "Otro" y "Telnet" estén seleccionados en la sección "Tipo de conexión". El puerto predeterminado 23 es correcto).
podklyuchenie-cherez-masilla-k-televizoru-lg-telnet.jpg
y ejecuta los siguientes comandos (puedes copiar y pegar todos a la vez haciendo clic derecho o presionando Shift + Insertar, no olvides presionar Enter después):
CÓDIGO: SELECCIONAR TODO
unset LD_PRELOAD
/media/developer/apps/usr/palm/services/org.webosbrew.hbchannel.service/elevate-service
mkdir -p /var/lib/webosbrew/init.d
cp /media/developer/apps/usr/palm/services/org.webosbrew.hbchannel.service/startup.sh /var/lib/webosbrew/startup.sh
rm -rf /var/luna/preferences/devmode_enabled && mkdir -p /var/luna/preferences/devmode_enabled

9. Elimine la aplicación del modo de desarrollador. Debe hacer esto o ssh no funcionará;

10. En tipo masilla
CÓDIGO: SELECCIONAR TODO
reboot

11. Una vez que su televisor se haya reiniciado, inicie el canal Homebrew nuevamente y haga clic en el icono de engranaje (configuración). Debería ver Root status ok , lo que indica que el canal Homebrew tiene acceso de root.
lg-webos-tv-homebrew-channel-settings-root-status-ok.jpg
Ahora puede habilitar el servidor SSH alternando su interruptor.
homebrew-channel-settings-raíz-configuración.jpg

Una vez hecho esto, haga clic en "Reinicio del sistema" (abajo a la izquierda) para reiniciar su televisor. Eso es todo, se recibe la raíz;

12. Una vez que se hayan realizado las manipulaciones, puede activar la descarga rápida de TV desde el elemento n. ° 2 y, en Homebrew Channel, bloquear el televisor para que no reciba actualizaciones para evitar perder la raíz (elemento Bloquear actualizaciones del sistema o con el comando ) .

Una vez rooteado, puede conectarse al televisor a través de SSH utilizando el nombre de usuario root , la contraseña alpine y el puerto 22 .

winscp-televizor-lg-ssh.jpg
La aplicación recomendada para trabajar con archivos en la TV es WinSCP.

Si tiene una conexión Telnet, pero no SSH (o WinSCP ), use la solución de aquí: romanvs777 @ [rootmy.tv] How to root webOS .
Creditos a JackSparrow(http://webos-forums.ru/jacksparrow-u8940.html)
