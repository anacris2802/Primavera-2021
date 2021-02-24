En eldocumento, deberás explicar en qué consiste tuproyecto,
qué funcionalidades tiene, 
cómo se debe utilizar o cualquierotro elemento que consideres importante para quienes visiten tu repositorio. 

especialmente cómo organizar un documento, escribirlo con mayor claridad, incorporar apoyos visuales y darle un formato profesional.
Incorpora en tu documento al menos dos apoyos visuales: un diagrama y un apoyo visual adicional de tu preferencia. 



# This is War!

El objetivo de este proyecto es simular una batalla de manera muy simple. Para hacerlo, se usan las [*Leyes de Lanchester*]:
  <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -ay ">
  
  <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx ">
  
  con condiciones iniciales  <img src="https://render.githubusercontent.com/render/math?math=x(0) = x_0"> y  <img src="https://render.githubusercontent.com/render/math?math=y(0) = y_0">.
    
    
Los supuestos básicos del proyecto fueron: 
* Hay dos contrincantes: azules y rojos
* Los principales factores que deciden el resultado de la batalla son el número de tropas y el entrenamiento/equipo.
* Se tomaron <img src="https://render.githubusercontent.com/render/math?math=x"> como el número de tropas de los rojos y <img src="https://render.githubusercontent.com/render/math?math=y"> como el número de tropas de los azules.
* Se tomaron <img src="https://render.githubusercontent.com/render/math?math=a"> como la potencia de fuego de los rojos y <img src="https://render.githubusercontent.com/render/math?math=b"> como la potencia de fuego de los azules.
* La potencia de fuego está basada en el entrenamiento, equipo, etc.

El Proyecto consta de distintos escenarios, cada uno con sus supuestos particulares. Las secciones en las que se divide es:
1) [Combate sencillo](#combate-sencillo)
2) [Combate entre guerrillas](#combate-entre-guerrillas)
3) [Vietnam](#vietnam)
4) [Combate convencional](#combate-convencional)
5) [Esparta](#esparta)


### Combate sencillo
En esta sección, los supuestos son los mismos a los generales. Las dos tropas conocen la ubicación del 'enemigo' y disparan con una potencia de fuego determinada previamente. 
##### Ecuaciones:
 <img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -ay ">
  
 <img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx ">



### Combate entre guerrillas

Este modelo representa el combate de 2 fuerzas que no tienen la ubicación de la fuerza contraria. Así mismo, no conocen el daño que han infligido al equipo contrario. Esto hará que concentren su fuego en una área determinada en la que creen que se encuentra el enemigo.

##### Ecuaciones:

<img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -axy"> 
<img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bxy"> 



### Vietnam
Este modelo es la unión del combate sencillo y del combate entre guerrillas. Una de las dos tropas es atacada por sopresa, de manera que la fuerza que embosca tiene más ventaja sobre la emboscada. Particularmente representa la batalla de EE.UU. y Vietcong. Aquí, Vietcong tiene la ventaja de ser 'local' y conocer el territorio por lo que toma el papel de fuerza 'emboscasora', mientras que EE.UU. es tomada por sopresa. 

Con este escenario, podemos ver que las fuerzas pequelas pueden tener una ventaja sobre las fuerzas grandes cuando se les ataca por sorpresa. 

##### Ecuaciones
<img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = -axy"> 
<img src="https://render.githubusercontent.com/render/math?math=\frac{dy}{dt} = -bx"> 


### Combate convencional
Es posible modificar las ecuaciones para modelar combate convencional (CONCON):$$
\frac{dx}{dt} = -cx-ay+P(t)
$$$$
\frac{dy}{dt} = -bx-dy+Q(t)
$$donde ${d,c}$ son la tasa de pérdidas operacionales (enfermedades, deserciones, etc.) -proporcional al número de las tropas, y ${a,b}$ es la tasa de pérdidas en combate. ${P,Q}$ es la tasa de refuerzos. La batalla de Iwo Jima, en la segunda guerra mundial, fué modelada por Engel en 1954, aplicando estas ecuaciones y dió una comprobación empírica de las ecuaciones de Lanchester, aunque en este caso, sólo el ejército de EUA tuvo refuerzos:$$
\frac{dx}{dt} = -ay
$$$$
\frac{dy}{dt} = -bx+Q(t)
$$Resuelva las ecuaciones con $x_0 = 21,500$, $y_0=0$ y$$Q(t) = 54,000 \mathcal{U}_{[0,1]} + 6,000 \mathcal{U}_{[2_3]} + 13,000 \mathcal{U}_{[5,6]},$$donde $\mathcal{U}$ es la función escalón.
### Esparta
Es posible simular la batalla del Termópilas: Suponga que sólo $C$ unidades de cada lado caben en el estrecho (o paso) de Termópilas, entonces las ecuaciones se convierten en$$
\frac{dx}{dt} = -a \min(y,C)
$$$$
\frac{dy}{dt} = -b \min(x,C)
$$Separe en cuatro casos el espacio $x-y$ y dibuje las regiones de manera analítica. ¿Obtiene el mismo resultado numérico? Utilice los datos "históricos" ¿El resultado es parecido a la vida real?
Agentes Use la clase agente para modelar el último escenario, suponga únicamente combate cuerpo a cuerpo, asigne una probabilidad de herir, morir y matar para los agentes que estén uno enfrente de otro. Agregue un valor de cohesión / miedo. Si pasa de un límite el miedo huye el agente. Agregue un atributo de moral. ¿Los resultados coinciden con el modelo de Lanchester?




[*Leyes de Lanchester*]:https://es.wikipedia.org/wiki/Leyes_de_Lanchester#:~:text=Las%20leyes%20de%20Lanchester%20(en,fuego%20en%20funci%C3%B3n%20del%20tiempo.
