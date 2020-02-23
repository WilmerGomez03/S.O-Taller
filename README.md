## S.O-Taller
# 1.

```New-Item -ItemType File -Name "fileATaller.txt" -Value "datos1 ndato2 ndato3"
```New-Item -ItemType File -Name "fileBTaller.txt" -Value "datos0 ndato2 ndato4"
InputObject SideIndicator
----------- -------------
datos0      =>           
dato4       =>           
datos1      <=           
dato3       <=           
# 2. Si se ejecuta el comando get-service | export-csv servicios.csv | ```out-file se genera un error, porque el cmlet out-file tiene un parametro requerido el cual es el Filepath el cual le indica el destino al cual enviara la informacion es decil le da el camino del archivo donde se escribira la informacion del get-service #3. con el parametro -Delimiter y entre comillas el ;

# 4. 
para evitar sobreescritura se agrega el parametro -NoClobber o -NoOverwrite
#5.
Con el paramtro -UseCulture
#6.
```get-Random genera un número aleatorio
#7.
```get-Date
#8.
  un objeto tipo DateTime
#9.
```get-date | Select-Object -Property DayOfWeek
  DayOfWeek
  ---------
   Saturday

#10.
```get-HotFix

#11.
```Get-HotFix | Select-Object -Property InstalledOn , HotFixID , InstalledBy | Sort-Object -Property InstalledOn

#12.
```Get-HotFix | Select-Object -Property  Description, HotFixID, InstalledOn  | Sort-Object -Property Description | ConvertTo-Html > hotfix.html
#13.
```Get-EventLog -Newest 50 -LogName System | Select-Object -Property Index ,TimeGenerated , Source | Sort-Object -Descending -Property @{Expression = "TimeDecendig"; Descending = $True}, @{Expression = "Index"; Descending = $False}
