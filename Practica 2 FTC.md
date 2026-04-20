1. ¿En qué se diferencian los lenguajes recursivos, los lenguajes recursivamente numerables no recursivos y los lenguajes no recursivamente numerables?

	 **Lenguajes Recursivos (R)**: Son lenguajes para los cuales existe una Máquina de Turing (MT)
	que los acepta y siempre se detiene. Esto significa que para cualquier cadena de entrada w, la MT determinará si w pertenece o no al lenguaje y siempre dará una respuesta (aceptando o rechazando).
	
	**Lenguajes Recursivamente Enumerables no Recursivos (RE - R):** Son lenguajes para los
	cuales existe una MT que los acepta. Sin embargo, esta MT no siempre se detiene para las
	cadenas que no pertenecen al lenguaje. Si una cadena w está en el lenguaje, la MT la
	aceptará y se detendrá. Pero si w no está en el lenguaje, la MT podría rechazar y detenerse o
	entrar en un bucle infinito.
	
	**Lenguajes No Recursivamente Enumerables:** Estos lenguajes son aquellos para los cuales no existe una MT que los acepte.

2. Probar que R  C_ RE  C_ 𝔏. Ayuda: usar las definiciones. 

	L: Un lenguaje con alfabeto Ʃ es un conjunto de cadenas finitas de símbolos de Ʃ.
	
	𝔏: Es el conjunto universal de todos los lenguajes con alfabeto Ʃ: conjunto de todos los
	subconjuntos de Ʃ*.
	
	Un lenguaje L es recursivo (L ∈ R) si existe una MT M que lo acepta y siempre para (lo
	decide).
	
	Un lenguaje L es recursivamente enumerable (L ∈ RE) si existe una MT M que lo acepta.


	R ⊆ RE: Si un lenguaje L es recursivo, es decir, (L ∈ R), entonces por definición existe una MT M que lo acepta y siempre se detiene. Esta misma MT M también cumple con la definición de un lenguaje recursivamente enumerable (existe una MT M que lo acepta y se detiene en ese caso).
	La condición adicional para los lenguajes recursivos es que la MT M también debe detenerse
	para las entradas que no están en el lenguaje, lo cual no contradice la definición de un lenguaje recursivamente enumerable. Por lo tanto, todo lenguaje recursivo es también un lenguaje recursivamente enumerable.

	RE ⊆ 𝔏: Si un lenguaje L es recursivamente enumerable (L ∈ RE), entonces por definición, existe una MT M que lo reconoce. El conjunto de cadenas aceptadas por una MT define un lenguaje. Dado que todo lenguaje recursivamente enumerable es un conjunto de cadenas sobre algún alfabeto (el lenguaje aceptado por una MT), **todo lenguaje recursivamente enumerable es también un lenguaje, y por lo tanto pertenece al conjunto de todos los lenguajes 𝔏.



3. Dijimos en clase que el hecho de que si L es recursivo entonces LC también lo es, significa
en términos de problemas que si un problema es decidible entonces también lo es el
problema contrario. ¿Qué significa en términos de problemas que la intersección de dos
lenguajes recursivos es también un lenguaje recursivo?

En términos de problemas, que la intersección de dos lenguajes recursivos (L1 ∩ L2) sea
también un lenguaje recursivo significa que si tenemos dos problemas que son decidibles
individualmente, entonces el problema que consiste en determinar si una instancia dada es una
instancia positiva para ambos problemas, también es decidible.
Más específicamente:

Si L1 es un lenguaje recursivo, representa un problema P1 que es decidible. Esto significa
que existe una Máquina de Turing M1 que siempre se detiene y determina si una instancia
dada pertenece o no a las instancias positivas de P1.

Si L2 es un lenguaje recursivo, representa un problema P2 que es decidible. Esto significa
que existe una Máquina de Turing M2 que siempre se detiene y determina si una instancia
dada pertenece o no a las instancias positivas de P2.

La intersección L1 ∩ L2 representa el problema P1∩2 cuya instancia positiva es aquella que es
instancia positiva tanto para P1 como para P2.

El hecho de que L1 ∩ L2 sea recursivo implica que existe una Máquina de Turing M que
siempre se detiene y decide si una instancia dada es positiva tanto para P1 como para P2.

Esta Máquina de Turing M puede lograr esto ejecutando secuencialmente M1 y M2 sobre la
misma entrada. M aceptará la entrada solo si tanto M1 como M2 la aceptan (lo que indica
que la instancia es positiva para ambos problemas). En cualquier otro caso (si M1 rechaza o
M2 rechaza), M rechazará. Dado que tanto M1 como M2 siempre se detienen, M también
siempre se detendrá, demostrando que P1∩2 es decidible.

![[Pasted image 20260317131650.png]]


En resumen, la propiedad de cierre de los lenguajes recursivos bajo la operación de intersección
se traduce a que si podemos decidir dos problemas por separado, también podemos decidir
el problema que requiere que ambas condiciones de los problemas originales se cumplan
simultáneamente.


4. Explicar por qué no es correcta la siguiente prueba de que si L ∈ RE, también LC ∈ RE: dada
una MT M que acepta L, entonces la MT M’, igual que M pero con los estados finales
permutados, acepta L^c


Definiciones a tener en cuenta

El complemento de un lenguaje L, denotado como L^c  contiene todas las cadenas sobre el
alfabeto que no están en L.

La prueba que se propone para demostrar que si L ∈ RE, entonces LC ∈ RE es incorrecta
debido a la naturaleza de los lenguajes recursivamente enumerables (RE) y el comportamiento
de las Máquinas de Turing (MT) que los aceptan.
Tomamos una MT M que acepta L y creamos una nueva MT M ′ que es idéntica a M excepto
que sus estados de aceptación (qA) y rechazo (qR) están permutados. La idea es que si M acepta
w (porque w ∈ L), entonces M ′ rechazaría w. Y si M rechazaba w (porque w ∉ L), entonces M ′
aceptaría w.
El problema fundamental con esta prueba radica en la posibilidad de que la MT M no se
detenga para las entradas w ∉ L.
