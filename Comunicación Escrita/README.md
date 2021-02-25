# This is War!

El objetivo de este proyecto es simular distintos escenarios de batalla utilizando ecuaciones diferenciales implementadas en Python. 

---
# Contenido:

* [Información general](*información-general)
* [Escenarios](*escenarios)
* [Técnicas usadas](*técnicas-usadas)
* [Ejemplo de uso](*ejemplo-de-uso)
    
    
---
## Información general
Para modelar las batallas, se usan las [*Leyes de Lanchester*]:

  <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -ay ">
  
  <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx ">
  
  con condiciones iniciales  <img src="https://render.githubusercontent.com/render/math?math=x(0) = x_0"> y  <img src="https://render.githubusercontent.com/render/math?math=y(0) = y_0">.
  
Los supuestos básicos del proyecto son: 
* Hay dos contrincantes: azules y rojos
* Los principales factores que deciden el resultado de la batalla son el número de tropas y el entrenamiento/equipo.
* Se tomaron <img src="https://render.githubusercontent.com/render/math?math=x"> como el número de tropas de los rojos y <img src="https://render.githubusercontent.com/render/math?math=y"> como el número de tropas de los azules.
* Se tomaron <img src="https://render.githubusercontent.com/render/math?math=a"> como la potencia de fuego de los rojos y <img src="https://render.githubusercontent.com/render/math?math=b"> como la potencia de fuego de los azules.
* La potencia de fuego está basada en el entrenamiento, equipo, etc.

---
## Escenarios
El Proyecto consta de distintos escenarios, cada uno con sus supuestos particulares. Las secciones en las que se divide son:
1) [Combate sencillo](#combate-sencillo)
2) [Combate entre guerrillas](#combate-entre-guerrillas)
3) [Vietnam](#vietnam)
4) [Combate convencional](#combate-convencional)
5) [Esparta](#esparta)


### Combate sencillo
En esta sección, los supuestos son los mismos a los generales. Las dos tropas conocen la ubicación del 'enemigo' y disparan con una potencia de fuego determinada previamente. 
##### Ecuaciones:
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -ay ">
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx ">



### Combate entre guerrillas

Este modelo representa el combate de 2 fuerzas que no tienen la ubicación de la fuerza contraria. Así mismo, no conocen el daño que han infligido al equipo contrario. Esto hará que concentren su fuego en una área determinada en la que creen que se encuentra el enemigo.

##### Ecuaciones:

* <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -axy"> 
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bxy"> 



### Vietnam
Este modelo es la unión del combate sencillo y del combate entre guerrillas. Una de las dos tropas es atacada por sopresa, de manera que la fuerza que embosca tiene más ventaja sobre la emboscada. Particularmente representa la batalla de EE.UU. y Vietcong. Aquí, Vietcong tiene la ventaja de ser 'local' y conocer el territorio por lo que toma el papel de fuerza 'emboscasora', mientras que EE.UU. es tomada por sopresa. 

Con este escenario, podemos ver que las fuerzas pequelas pueden tener una ventaja sobre las fuerzas grandes cuando se les ataca por sorpresa. 

##### Ecuaciones

* <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -axy"> 
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx"> 


### Combate convencional

Aquí tomamos el supuesto de que la tropas pueden recibir refuerzos. Usamos una función escalonada para modelar el número de refuerzos que llegan en cierto perodo de tiempo. Gracias a esto, los resultados de las batallas se ven más realistas a las que conocemos. 

##### Ecuaciones

* <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -cx-ay+P(t)"> 
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx-dy+Q(t)"> 

donde <img src="https://render.githubusercontent.com/render/math?math={d,c}">son la tasa de pérdidas operacionales (enfermedades, deserciones, etc.) -proporcional al número de las tropas, y <img src="https://render.githubusercontent.com/render/math?math={a,b}"> es la tasa de pérdidas en combate. <img src="https://render.githubusercontent.com/render/math?math={P,Q}"> es la tasa de refuerzos. 


### Esparta

Aquí se simula la batalla de Termópilas. Se supone que solo <img src="https://render.githubusercontent.com/render/math?math=C"> unidades de cada lado caben en el estrecho de Termópilas, por lo que las ecuaciones ahora solo toman el mínimo entre la cantidad de tropas <img src="https://render.githubusercontent.com/render/math?math=y"> y <img src="https://render.githubusercontent.com/render/math?math=C">.

##### Ecuaciones

* <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -a \min(y,C)"> 
* <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -b \min(x,C)"> 




---
## Técnicas usada

El proyecto toca varios temas dentro del propóstio principal que es modelar batallas. Estos temas son:

* [Resolución de ecuaciones diferenciales](#resolución-de-ecuaciones-diferenciales)
* [Visualización de un proceso a través del tiempo](#visualización-de-un-proceso-a-través-del-tiempo)
* [Graficación interactiva](#graficación-interactiva)
* [Modelación usando agentes](#modelación-usando-agentes)

Todos estos temas pudieron ocuparse gracias a las siguientes librerias de Python:
* [NumPy](https://numpy.org/doc/stable/user/whatisnumpy.html)
* [SimPy](https://simpy.readthedocs.io/en/latest/)
* [Matplotlib](https://matplotlib.org/stable/index.html)
* [iPyWidgets](https://ipywidgets.readthedocs.io/en/stable/examples/Widget%20Basics.html)
* [IPython.display](https://ipython.org/ipython-doc/stable/api/generated/IPython.display.html)

### Resolución de ecuaciones diferenciales
El resolver ecuaciones diferenciales de primer orden es uno de los temas centrales del proyecto. Para esto se usa el método `dsolve(ode)` incluido en la libreria *SimPy*. Un ejemplo del código es este: 
```python
ode1 = Eq(dx,-a*y1(t))    # Declaramos la ecuación diferencial que queremos resolver
dsolve(ode1)              # Resolvemos con el método de SimPy

```
Ejecutando este código nos da el resultado de la `ode1` planteada. 

Es así como todo el proyecto puede resolverse de una manera práctica y rápida, sin el cansancio de tener que hacer todas las ecuaciones a mano. 


### Visualización de un proceso a través del tiempo

### Graficación interactiva
### Modelación usando agentes
Agentes Use la clase agente para modelar el último escenario, suponga únicamente combate cuerpo a cuerpo, asigne una probabilidad de herir, morir y matar para los agentes que estén uno enfrente de otro. Agregue un valor de cohesión / miedo. Si pasa de un límite el miedo huye el agente. Agregue un atributo de moral. ¿Los resultados coinciden con el modelo de Lanchester?

---
## Ejemplo de uso


[*Leyes de Lanchester*]:https://es.wikipedia.org/wiki/Leyes_de_Lanchester#:~:text=Las%20leyes%20de%20Lanchester%20(en,fuego%20en%20funci%C3%B3n%20del%20tiempo.
