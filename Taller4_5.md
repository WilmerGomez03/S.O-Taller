# Taller powershell modulo 4 y 5
## Modulo 4 comandos 
###### archivo transcript en el repositorio
	
1. Mostrar una tabla de procesos que incluya únicamente los nombres de los
   procesos, sus IDs, y si están respondiendo a Windows (la propiedad
   ``Responding`` muestra eso). Haga que la tabla tome el mínimo de espacio
   horizontal, pero no permita que la información se trunque.
   
   > PS C:\Users\Andres gomez> Get-Process | Select-Object -Property ID,Responding | ft -Property * -AutoSize -Wrap

2. Muestre una tabla de procesos que incluya los nombres de los procesos y sus
   IDs. También incluya columnas para uso de memoria virtual y física;
   exprese dichos valores en megabytes (MB).
   
   > Get-Process | Select-Object -Property ID,name,vm,pm | ft -Property ID,Name,@{n='Memoria virtual (MB)';e={$_.VM / 1MB -as [int]}},@{n='Memoria fisica (MB)';e={$_.PM / 1MB -as [int]}} -AutoSize -Wrap

3. Emplee ``Get-EventLog`` para mostrar una lista de los logs de eventos
   disponibles (revise la ayuda para encontrar el parámetro que le permitirá
   obtener dicha información). Formatee la salida como una tabla que incluya
   el nombre de despliegue del log y el período de retención. Los encabezados
   de columna deben ser NombreLog y Per-Retencion.
   
   > get-eventlog -list | select-object log,MinimumRetentionDays | ft -Property @{n='NombreLog';e={$_.log}},@{n='Per-Retention';e={$_.MinimumRetentionDays}}
   

4. Muestre una lista de servicios, de tal manera que aparezcan agrupados los
   servicios que están iniciados y los que están detenidos. Los que están
   iniciados deben aparecer primero.
   
   > get-service | select-object -Property Name,Status |sort Status -Descending | fl -property * -groupby status

5. Mostrar una lista a cuatro columnas de todos los directorios que están en
   el raíz de la unidad ``C:``
   
   > ls -path C:\ | where -FilterScript {$_.Attributes -eq 'Directory'} | fw -Property name -col 4
   

6. Cree una lista formateada de todos los archivos ``.exe`` del directorio
   ``C:\Windows``. Debe mostrarse el nombre, la información de versión, y el
   tamaño del archivo. La propiedad de tamaño se llama ``length`` en Powershell,
   pero para mayor claridad, la columna se debe llamar **Tamaño** en su listado.
   
   > ls * .exe -Path C:\Windows |fl -Property @{n='Nombre';e={$_.Name}},@{n='Versión';e={$_.VersionInfo.FileVersion}},@{n='Tamaño (KB)';e={$_.Length / 1KB -as [int]}}
   
7. Importe el módulo ``NetAdapter`` (empleando el comando ``Import-Module
   NetAdapter``).
   Empleando el cmdlet ``Get-NetAdapter``, muestre una lista de adaptadores no
   virtuales (adaptadores cuya propiedad Virtual sea falsa. El valor lógico
   falso es representado por Powershell como ``$False``).
   
   > Import-Module NetAdapter
   > Get-NetAdapter | Select-Object -Property Name,Virtual | Where-Object -Filter {$_.Virtual -eq $false} | fl -Property *

8. Importe el módulo ``DnsClient``. Empleando el cmdlet ``Get-DnsClientCache``,
   muestre una lista de los registros ``A`` y ``AAAA`` que estén en el caché.
   Sugerencia: Si el caché está vacío, visite algunos sitios web para poblarlo.
   
   > Import-Module dnsclient
   > Get-DnsClientCache -Type A,AAAA | fl *

9. Genere una lista de todos los archivos ``.exe`` del directorio
   ``C:\Windows\System32`` que tengan más de 5 MB.
   
   > ls * .exe -path C:\Windows\System32 | where -FilterScript {$_.Length /1MB -gt 5 } | fl -Property name,@{n='Tamaño (MB)';e={$_.Length / 1MB -as [int]}}

10. Muestre una lista de parches que sean actualizaciones de seguridad.

   > Get-HotFix | where -FilterScript {$_.Description -eq 'Security update'} | fl -Property *


11. Muestre una lista de parches que hayan sido instalados por el
    usuario ``Administrador``, que sean actualizaciones. Si no tiene ninguno,
    busque parches instalados por el usuario ``System``. Note que algunos parches
    no tienen valor en el campo ``Installed By``.
    
    > Get-HotFix | where -FilterScript {$_.Installedby -like '*System*' -and $_.Description -like 'update'} | ft 
    
    > Get-HotFix | where -FilterScript {$_.Installedby -like '*System*' -and $_.Description -like 'update'} | fl 
    
    __*Nota:*__ *System* esta entre asteriscos pero el formato lo coloca en cursiva
    
12. Genere una lista de todos los procesos que estén corriendo con el nombre
    **Conhost** o **Svchost**.
    >Get-process | Where {$_.Name -like 'Svchost*' -or $_.Name -like 'Conhost*'} | ft -Property id ,ProcessName, Description -Wrap -AutoSize
    
## Modulo 5 comandos

1. ¿Cuál clase puede emplearse para consultar la dirección IP de un adaptador
   de red? ¿Posee dicha clase algún método para liberar un préstamo de
   dirección (lease) DHCP?
   
   >Get-WmiObject -Namespace root\CIMv2 -class win32_networkAdapterconfiguration | Get-member
   
   >Get-WmiObject -Namespace root\CIMv2 -class win32_networkAdapterconfiguration | Select-Object IP
   
   Exite el metodo RenewDHCPLease o ReleaseDHCPLease 
  
2. Despliegue una lista de parches empleando WMI (Microsoft se refiere a los
   parches con el nombre **quick-fix engineering**). Es diferente el listado al
   que produce el cmdlet ``Get-Hotfix``?
   
   >Get-WmiObject -Namespace root\CIMv2 -class Win32_QuickFixEngineering
   
   no hay diferencia con respecto al listado generado por ambos cmdlet
   
3. Empleando WMI, muestre una lista de servicios, que incluya su status actual,
   su modalidad de inicio, y las cuentas que emplean para hacer login.
   
   >Get-WmiObject -Namespace ROOT\CIMV2 -Class Win32_Service | Select-Object name, Status,StartMode,Startname | fl *
   >Get-WmiObject -Namespace ROOT\CIMV2 -Class Win32_Service | Select-Object name, Status,StartMode,Startname | ft *
   
4. Empleando cmdlets de CIM, liste todas las clases del namespace
   ``SecurityCenter2``, que tengan **product** como parte del nombre.
   
   > Get-CimClass -Namespace root\SecurityCenter2 | where cimclassname -Like '*product*'
   
   	__*Nota:*__ *product* esta entre asteriscos pero el formato lo coloca en cursiva
	
   > Get-CimClass -Namespace root\SecurityCenter2 -ClassName *product* | Select-Object *  
   
5. Empleando cmdlets de CIM, y los resultados del ejercicio anterior, muestre
   los nombres de las aplicaciones antispyware instaladas en el sistema.
   También puede consultar si hay productos antivirus instalados en el sistema.
   
   > Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntiSpywareProduct | fl -Property displayName,productState,timestamp

   > Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntiVirusProduct | fl -Property displayName,productState,timestamp
   
