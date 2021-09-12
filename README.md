### Overview of the solution

```python
# Author: Guillermo Castillo
#Function that calculates the payment for a given hour
#According to the different hourly rates
def calcularPago(hora, pagoH1, pagoH2, pagoH3):
    #Calcula el total de horas trabajadas
    if (int(hora[1][0:2]) == 0):
        totalHoras = 24 - int(hora[0][0:2])
    else:
        totalHoras = int(hora[1][0:2]) - int(hora[0][0:2])
    #Determines the payment according to the range of established schedules
    if (0 <= int(hora[0][0:2]) < 9):
        if (0 < int(hora[1][0:2]) <= 9):
            pagoTotal = totalHoras * pagoH1
        elif (9 < int(hora[1][0:2]) <= 18):
            resto = int(hora[1][0:2]) - 9
            totalHoras -= resto
            pagoTotal = (totalHoras * pagoH1) + (resto * pagoH2)
        elif (18 < int(hora[1][0:2]) <= 23 or int(hora[1][0:2]) == 0):
            if (int(hora[1][0:2]) == 0):
                resto = 6
            else:
                resto = int(hora[1][0:2]) - 18
            totalHoras -= (resto + 9)
            pagoTotal = (totalHoras * pagoH1) + (9 * pagoH2) + (resto * pagoH3)

    elif (9 <= int(hora[0][0:2]) < 18):
        if (9 < int(hora[1][0:2]) <= 18):
            pagoTotal = totalHoras * pagoH2
        elif (18 < int(hora[1][0:2]) <= 23 or int(hora[1][0:2]) == 0):
            if (int(hora[1][0:2]) == 0):
                resto = 6
            else:
                resto = int(hora[1][0:2]) - 18
            totalHoras -= resto
            pagoTotal = (totalHoras * pagoH2) + (resto * pagoH3)

    else:
        pagoTotal = totalHoras * pagoH3
    return pagoTotal

#Opens the .txt file for data reading
f = open ('ACMEdata.txt', 'r')
for linea in f:
    listaLinea = linea.strip("\n").split("=")
    pagoTotal = 0
    for dato in listaLinea[1].split(","):
        hora = dato[2:].strip().split("-")
        #Determines which day of the week is being analyzed.
        if (dato[0:2] == "MO" or dato[0:2] == "TU" or dato[0:2] == "WE" or dato[0:2] == "TH" or dato[0:2] == "FR"):
            #The function created to obtain the payment for that day is called
            pagoTotal += calcularPago(hora, 25, 15, 20)
        elif (dato[0:2] == "SA" or dato[0:2] == "SU"):
            pagoTotal += calcularPago(hora, 30, 20, 25)
        else:
            print("Invalid day\n" + "Correct the file for: " + listaLinea[0])
            exit()
    print("The amount to pay " + listaLinea[0] + " is: "+ str(pagoTotal) + " USD\n")
#The .txt file is closed
f.close()
input("Press enter to close the program")
```
### Arquitecture
In the code, a function was made to calculate the payment for a given work schedule. Then the .txt file is opened for reading, and it is determined data by data the day that was worked to then call the function created and obtain the respective total payment per hour. And in case a day is misspelled, the program stops and informs which employee has the error. In addition, an "input" was put at the end of the code with the only purpose of keeping the window of the .exe file open until the user wants it.
### Approach and Methodology
Employees'pay was required to be calculated according to their number of hours worked, which in turn depended on the day on which they worked. The information was in a .txt file, and therefore a program was made in Python programming language, which was converted to an executable file so that anyone can use the program, without needing any IDE. 
### How to run the program locally
##### For windows:
-Download "dist" folder
-Execute the .exe file
-You can also edit the .txt file to make different tests
##### For other OS:
-Please copy the given code to your preferred IDE
