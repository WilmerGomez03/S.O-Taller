# Taller powershell modulo 4 y 5
## Modulo 4
###### transcript
	**********************
	Inicio de la transcripción de Windows PowerShell
	Hora de inicio: 20200323103339
	Nombre de usuario: APC\Andres gomez
	Usuario RunAs: APC\Andres gomez
	Nombre de la configuración: 
	Máquina: APC (Microsoft Windows NT 10.0.18362.0)
	Aplicación host: C:\WINDOWS\system32\WindowsPowerShell\v1.0\PowerShell_ISE.exe
	Id. de proceso: 11808
	PSVersion: 5.1.18362.628
	PSEdition: Desktop
	PSCompatibleVersions: 1.0, 2.0, 3.0, 4.0, 5.0, 5.1.18362.628
	BuildVersion: 10.0.18362.628
	CLRVersion: 4.0.30319.42000
	WSManStackVersion: 3.0
	PSRemotingProtocolVersion: 2.3
	SerializationVersion: 1.1.0.1
	**********************
	La transcripción ha comenzado. El archivo de salida es E:\Semestre 8\SO_powershell\taller4_5.txt
1. Mostrar una tabla de procesos que incluya únicamente los nombres de los
   procesos, sus IDs, y si están respondiendo a Windows (la propiedad
   ``Responding`` muestra eso). Haga que la tabla tome el mínimo de espacio
   horizontal, pero no permita que la información se trunque.
   > PS C:\Users\Andres gomez> Get-Process | Select-Object -Property ID,Responding | ft -Property * -AutoSize -Wrap
	   Id Responding
	   -- ----------
	  956       True
	10568       True
	 9264       True
	 7232       True
	13944       True
	12104       True
	 4156       True
	10900       True
	11716       True
	 2424       True
	 3200       True
	 5184       True
	 5220       True
	 7620       True
	 7996       True
	 9632       True
	 9640       True
	10852       True
	13368       True
	13600       True
	13608       True
	14356       True
	15272       True
	 4772       True
	13848       True
	  820       True
	13688       True
	10276       True
	 5760       True
	13332       True
	13972       True
	 4016       True
	10316       True
	 1096       True
	14248       True
	 4116       True
	    0       True
	 1908       True
	12172       True
	11788       True
	 7268       True
	 5008       True
	 3304       True
	 4376       True
	 5652       True
	  736       True
	 5440       True
	 9392       True
	11808       True
	 6440       True
	 8540       True
	 2932       True
	   96       True
	 3896       True
	 4468       True
	 4624       True
	 7040       True
	13732       True
	10200       True
	  748       True
	 1944       True
	 4132       True
	13620       True
	  568       True
	 3052       True
	 3724       True
	 4252       True
	 8380       True
	  908       True
	 1044       True
	 1068       True
	 1088       True
	 1252       True
	 1308       True
	 1448       True
	 1460       True
	 1504       True
	 1556       True
	 1600       True
	 1672       True
	 1796       True
	 1852       True
	 1892       True
	 1900       True
	 1976       True
	 2068       True
	 2084       True
	 2112       True
	 2140       True
	 2184       True
	 2216       True
	 2268       True
	 2276       True
	 2468       True
	 2532       True
	 2584       True
	 2652       True
	 2732       True
	 2736       True
	 2836       True
	 2948       True
	 2956       True
	 3020       True
	 3084       True
	 3312       True
	 3320       True
	 3380       True
	 3424       True
	 3604       True
	 3760       True
	 3876       True
	 3884       True
	 4036       True
	 4044       True
	 4056       True
	 4104       True
	 4400       True
	 4440       True
	 4668       True
	 4704       True
	 4812       True
	 5092       True
	 5236       True
	 5276       True
	 5284       True
	 5536       True
	 6136       True
	 6156       True
	 6300       True
	 6484       True
	 6644       True
	 6856       True
	 7076       True
	 7292       True
	 7356       True
	 8360       True
	 8708       True
	 8776       True
	 9496       True
	 9688       True
	10512       True
	10948       True
	13632       True
	13788       True
	15176       True
	    4       True
	 2324       True
	 4288       True
	 4280       True
	 4124       True
	 4324       True
	14344       True
	  940       True
	14100       True
	 5532       True
	 6296       True
	10616       True
	 1160       True
	  624       True
   	

2. Muestre una tabla de procesos que incluya los nombres de los procesos y sus
   IDs. También incluya columnas para uso de memoria virtual y física;
   exprese dichos valores en megabytes (MB).

3. Emplee ``Get-EventLog`` para mostrar una lista de los logs de eventos
   disponibles (revise la ayuda para encontrar el parámetro que le permitirá
   obtener dicha información). Formatee la salida como una tabla que incluya
   el nombre de despliegue del log y el período de retención. Los encabezados
   de columna deben ser NombreLog y Per-Retencion.

4. Muestre una lista de servicios, de tal manera que aparezcan agrupados los
   servicios que están iniciados y los que están detenidos. Los que están
   iniciados deben aparecer primero.

5. Mostrar una lista a cuatro columnas de todos los directorios que están en
   el raíz de la unidad ``C:``

6. Cree una lista formateada de todos los archivos ``.exe`` del directorio
   ``C:\Windows``. Debe mostrarse el nombre, la información de versión, y el
   tamaño del archivo. La propiedad de tamaño se llama ``length`` en Powershell,
   pero para mayor claridad, la columna se debe llamar **Tamaño** en su listado.

7. Importe el módulo ``NetAdapter`` (empleando el comando ``Import-Module
   NetAdapter``).
   Empleando el cmdlet ``Get-NetAdapter``, muestre una lista de adaptadores no
   virtuales (adaptadores cuya propiedad Virtual sea falsa. El valor lógico
   falso es representado por Powershell como ``$False``).

8. Importe el módulo ``DnsClient``. Empleando el cmdlet ``Get-DnsClientCache``,
   muestre una lista de los registros ``A`` y ``AAAA`` que estén en el caché.
   Sugerencia: Si el caché está vacío, visite algunos sitios web para poblarlo.

9. Genere una lista de todos los archivos ``.exe`` del directorio
   ``C:\Windows\System32`` que tengan más de 5 MB.

10. Muestre una lista de parches que sean actualizaciones de seguridad.

11. Muestre una lista de parches que hayan sido instalados por el
    usuario ``Administrador``, que sean actualizaciones. Si no tiene ninguno,
    busque parches instalados por el usuario ``System``. Note que algunos parches
    no tienen valor en el campo ``Installed By``.

12. Genere una lista de todos los procesos que estén corriendo con el nombre
    **Conhost** o **Svchost**.
