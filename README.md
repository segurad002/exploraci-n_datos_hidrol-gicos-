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

### Se renombran los datos importados
```R
names(inp) <- c("fecha","estrella", "banano")
attach(inp)
```
_Utilizamos la funcion ```attatch``` para definir los nombres de los ríos_  

### Graficos los datos de estrella
```R
plot(estrella, xlab = "Puntos historicos")
```
![image](https://user-images.githubusercontent.com/82825982/119066403-eef4f600-b99c-11eb-8606-2df0c9fe2288.png)

### Procedemoa a tratar los datos para generar varias reprecentaciones
```R
Tempdate <- strptime(inp[,1], format= "%d/%m/%Y")
MAQ_estrella <- tapply(estrella, format(Tempdate, format= "%Y"), FUN=sum)
MAQ_banano <- tapply(banano, format(Tempdate, format= "%Y"), FUN=sum)

write.csv(rbind(MAQ_estrella,MAQ_banano),file="MAQ.csv")
```
_Con la funcion ```strptime``` especificamos el formato en que se encuetra la fecha de los datos._  
_La funcion ```tapply``` y sus parametros nos permite sumar los datos y agruparlos por año._  
_Por ultimo, combinamos los datos agrupados de banano y estrella utilizando ```rbind``` y los guardamos en un archivo **csv**._

#### Hidrografia del rio Banano vs Estrella
```R
plot(MAQ_banano, ylim=c(100,3000), xlab = "Años", ylab = "Hidrografia", main = "Rio Banano vr Estrella")
lines(MAQ_estrella, col=2)
```
![image](https://user-images.githubusercontent.com/82825982/119068223-f74f3000-b9a0-11eb-845b-12ec3d430254.png)

### Agrupamos los datos por meses del año
```R
plot(MAQ_banano, ylim=c(100,3000), xlab = "Meses", ylab = "Hidrografia", main = "Rio Banano vs Estrella")
lines(MAQ_estrella, col=2)
```
![image](https://user-images.githubusercontent.com/82825982/119068288-1fd72a00-b9a1-11eb-887f-801ef3030858.png)

### Analisis de correlación 
```R
conrip <- cor(inp[,2:3], method = "spearman")
conrip
plot(estrella,banano, main = "Correlación de datos entre ambos ríos")
```
_Con la funcion ```conrip``` generaramos una correlación entre los datos en estudio sobre los riós __Banano y Estrella__._  

![image](https://user-images.githubusercontent.com/82825982/119069193-e8697d00-b9a2-11eb-9db1-0059592b652e.png)  

### Graficos de correlaciónes específicas ríos Banano ~ Estrella
```R 
inp.lm <- lm(inp[,2] ~ inp[,3], data=inp)
summary(inp.lm)
plot(inp.lm, sub.caption = "Banano ~ Estrella")
```
_Luego de realizar un gráfico de correlación general se procede a identificar las correlación de acuerdo a los datos __residuales vs agrupados__, __Normal Q-Q__ Y __Escalas de localización__ para obtener una visualización más detalla_

#### Residual VS Equipado  
![image](https://user-images.githubusercontent.com/82825982/119070121-a2151d80-b9a4-11eb-9eff-4637ed326ec4.png)

#### Normal Q-Q  
![image](https://user-images.githubusercontent.com/82825982/119070170-b527ed80-b9a4-11eb-98f7-53862ef1d4be.png)

#### Escala de localización 
![image](https://user-images.githubusercontent.com/82825982/119070238-d557ac80-b9a4-11eb-8a1a-be1055186da4.png)



