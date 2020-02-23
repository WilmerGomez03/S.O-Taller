## S.O-Taller
#1. 
  - New-Item -ItemType File -Name "fileATaller.txt" -Value "datos1 `ndato2 `ndato3"
  - New-Item -ItemType File -Name "fileBTaller.txt" -Value "datos0 `ndato2 `ndato4"
  - ```diff -ReferenceObject (Get-Content .\fileATaller.txt) -DifferenceObject (Get-Content .\fileBTaller.txt)

    InputObject SideIndicator
    ----------- -------------
    datos0      =>           
    dato4       =>           
    datos1      <=           
    dato3       <=           
#2. 
  Si se ejecuta el comando ```get-service | ```export-csv servicios.csv | ```out-file se genera un error, porque el cmlet out-file tiene un parametro
  requerido el cual es el Filepath el cual le indica el destino al cual enviara la informacion es decil le da el camino del archivo donde se escribira
  la informacion del get-service
#3.
  con el parametro -Delimiter y entre comillas el ;
  ```export-csv servicios.csv -Delimiter ";"
#4. 
  para evitar sobreescritura se agrega el parametro -NoClobber o -NoOverwrite
#5.
  Con el paramtro -UseCult
