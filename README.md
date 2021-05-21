# Prueba practica tarea 2 



### Cargamos el directorio de trabajo
```R
setwd("C:/Users/Daniel Segura/Documents/UCR Segundo año/Procesamiento de datos geograficos/")
```

### Se importan los datos de los rios banano y estrella
```R
inp <- read.csv("FDC.csv", na.strings = "")
head(inp)
dim(inp)
```

_Utilizamos la funcion ```head``` para tener una vista previa de los datos_  
_ademas de utilizar ```dim``` para verificar la cantidad de datos_

### Limpiamos los datos que puedan estar vacios
```R
inp[!complete.cases(inp),]
```

### Hacemos una graficacion 
```R
plot(inp[,2], type = "l", col="blue", xlab = "Años", ylab = "Datos hidrografico", sub = "En azul datos para estrella y el verde para banano")
lines(inp[,3], col="green")
```
![image](https://user-images.githubusercontent.com/82825982/119064964-c15a7d80-b999-11eb-86f4-75a5c5d390e3.png)


### Hacemos una graficacion en barras individual para estrella y banano
```R
summary(inp[,2:3])
hist(inp[,2], main = "Histograma de estrella", xlab = "Hidrologia", ylab = "Frecuencia")
hist(inp[,3], main = "Histograma de banano", xlab = "Hidrologia", ylab = "Frecuencia")
```
![image](https://user-images.githubusercontent.com/82825982/119065454-ce2ba100-b99a-11eb-8e57-a84d43fb0d8c.png)

![image](https://user-images.githubusercontent.com/82825982/119065419-b3592c80-b99a-11eb-9608-0b1177459902.png)
