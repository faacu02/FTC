

Ejercicio 1. Responder breve y claramente los siguientes incisos:

a. ¿Por qué la complejidad temporal sólo trata los lenguajes recursivos?

La complejidad temporal mide la eficiencia de los algoritmos (cantidad de pasos de una Máquina de Turing). Solo se aplica a lenguajes **recursivos (decidibles)** porque estos garantizan que existe un algoritmo que **siempre se detiene** ante cualquier entrada. Si intentáramos medir la complejidad de un lenguaje no recursivo, la máquina podría entrar en un **loop infinito** para ciertas cadenas, haciendo que el tiempo de ejecución no esté definido.

b. Probar que n^3 = O(2n). Ayuda: hay que encontrar un número natural n0 y una constante c > 0 tales que n^3 <= c.2^n para todo n >= n0.

![[Pasted image 20260407164230.png]]

c. Probar que si T1(n) = O(T2(n)), entonces TIME(T1(n))  TIME(T2(n)). Ayuda: hay que probar
que si un lenguaje L está en TIME(T1(n)), también está en TIME(T2(n)) - recurrir
directamente a la definición de orden O de una función T y de clase TIME(T(n)) -.
d. ¿Cuándo un lenguaje pertenece a P, a NP y a EXP? ¿Por qué si un lenguaje pertenece a P
también pertenece a NP y a EXP?
e. ¿Qué formula la Tesis Fuerte de Church-Turing?
f. ¿Por qué es indistinta la cantidad de cintas de las MT que utilizamos para analizar los
lenguajes, en el marco de la jerarquía temporal que definimos?
g. ¿Qué codificación de cadenas se descarta en la complejidad temporal?
h. ¿Por qué si un lenguaje L pertenece a P, también su complemento LC pertenece a P?
Ayuda: hay que probar que si existe una MT M que decide L en tiempo poly(n), también
existe una MT M´ que decide LC en tiempo poly(n).
i. Sea L un lenguaje de NP. Explicar por qué los certificados de L miden un tamaño polinomial
con respecto al tamaño de las cadenas de entrada.