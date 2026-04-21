# Práctica 7 - FTC 2026
## Jerarquía Espacio-Temporal y Misceláneas

### Ejercicio 1. Responder breve y claramente:

**a. ¿Por qué en la complejidad espacial se utilizan MT con una cinta de entrada de sólo lectura?**
Se utiliza una cinta de entrada de sólo lectura para que el espacio ocupado por la entrada ($n$) no sea contabilizado en la medición del espacio utilizado por la máquina. Esto permite definir clases de complejidad con espacio sub-lineal, como **LOGSPACE** ($O(\log n)$), lo cual sería imposible si la entrada se considerara parte del espacio de trabajo (ya que ocuparía al menos $n$ celdas).

**b. ¿Por qué si una MT tarda tiempo poly(n) entonces ocupa espacio poly(n), y si ocupa espacio poly(n) puede llegar a tardar tiempo exp(n)?**
* **Tiempo poly(n) $\implies$ Espacio poly(n):** En cada paso de ejecución, el cabezal de la MT puede moverse a lo sumo una celda. Por lo tanto, en $T(n)$ pasos, la máquina no puede visitar más de $T(n)$ celdas distintas. Si el tiempo es polinomial, el espacio necesariamente lo es.
* **Espacio poly(n) $\implies$ Tiempo exp(n):** Una MT que utiliza espacio $S(n)$ tiene un número finito de configuraciones posibles (determinadas por los estados de control, las posiciones de los cabezales y el contenido de la cinta de trabajo). Para un alfabeto $\Gamma$ y $|Q|$ estados, el número de configuraciones es aproximadamente $|Q| \cdot n \cdot S(n) \cdot |\Gamma|^{S(n)}$. Si $S(n)$ es un polinomio, este número de configuraciones es exponencial. Si la máquina no entra en un bucle infinito, debe terminar en un tiempo proporcional al número de configuraciones, el cual es exponencial.

**c. ¿Por qué los lenguajes de la clase LOGSPACE son tratables?**
Los lenguajes de la clase LOGSPACE se consideran tratables porque **LOGSPACE $\subseteq$ P**. Como se vio en la clase (Slide 7), una máquina que ocupa espacio $O(\log n)$ tiene un número de configuraciones polinomial ($c^{\log n} = n^k$), por lo que su tiempo de ejecución es también polinomial. Al ser decidibles en tiempo polinomial, pertenecen a la clase P y se consideran tratables.

---

### Ejercicio 2. Describir la idea general de una MT que decida el lenguaje $L = \{a^n b^n \mid n \geq 1\}$ en espacio logarítmico.

Para decidir $L$ en espacio $O(\log n)$, la MT puede utilizar dos contadores en su cinta de trabajo:
1. **Contador i:** Recorre la cinta de entrada y cuenta la cantidad de símbolos 'a'.
2. **Contador j:** Recorre la cinta de entrada y cuenta la cantidad de símbolos 'b'.

**Algoritmo:**
1. Verificar que la entrada tenga el formato $a^* b^*$. Si no, rechaza.
2. Contar las 'a's incrementando el contador **i** en binario.
3. Contar las 'b's incrementando el contador **j** en binario.
4. Comparar los valores de **i** y **j**. Si son iguales y mayores o iguales a 1, acepta; de lo contrario, rechaza.

**Complejidad espacial:** Como el número total de símbolos es $n$, los contadores en binario ocupan a lo sumo $O(\log n)$ celdas cada uno. La cinta de entrada es de sólo lectura, por lo que el espacio total utilizado es logarítmico.

---

### Ejercicio 3. Describir la idea general de una MT que decida el lenguaje SAT en espacio polinomial.

Para decidir SAT (satisfacibilidad booleana) en espacio polinomial, podemos utilizar una MT determinista que pruebe todas las asignaciones posibles de manera secuencial.

**Idea general:**
1. Sea $\phi$ una fórmula con $m$ variables.
2. Para cada una de las $2^m$ posibles asignaciones de verdad:
   a. Generar la asignación en la cinta de trabajo. Esto ocupa espacio $O(m)$, que es polinomial respecto al tamaño de la fórmula.
   b. Evaluar la fórmula $\phi$ con dicha asignación. La evaluación de una fórmula booleana se puede realizar en tiempo (y por ende espacio) polinomial.
   c. Si la evaluación es verdadera, la MT **acepta**.
3. Si se probaron todas las asignaciones y ninguna satisfizo la fórmula, la MT **rechaza**.

**Espacio utilizado:** La MT solo necesita almacenar una asignación a la vez y el espacio necesario para la evaluación. Al reutilizar el mismo espacio para cada nueva asignación, el espacio total se mantiene en $O(poly(n))$.

---

### Ejercicio 4. Probar que NP $\subseteq$ PSPACE.

**Prueba:**
Sea $L \in NP$. Por definición, existe una MT verificadora $M_1$ que, dada una cadena $w$ y un certificado $x$, verifica si $w \in L$ en tiempo $poly(|w|)$. El tamaño del certificado $|x|$ también es $poly(|w|)$.

Podemos construir una MT $M_2$ que decida $L$ en espacio polinomial de la siguiente manera:
1. Dada una entrada $w$, $M_2$ recorre sistemáticamente todos los posibles certificados $x$ de tamaño hasta $poly(|w|)$.
2. Para cada certificado $x$:
   a. Ejecuta $M_1(w, x)$.
   b. Si $M_1$ acepta, $M_2$ **acepta**.
   c. Si $M_1$ rechaza, $M_2$ limpia el espacio utilizado por $x$ y pasa al siguiente certificado.
3. Si después de probar todos los posibles certificados ninguno fue aceptado, $M_2$ **rechaza**.

**Análisis de espacio:**
* Generar y almacenar un certificado $x$ requiere espacio $O(|x|) = O(poly(|w|))$.
* Ejecutar $M_1$ requiere espacio polinomial (ya que su tiempo es polinomial).
* Al reutilizar el espacio para cada intento de certificado, el espacio máximo utilizado en cualquier momento es polinomial. Por lo tanto, $L \in PSPACE$.

---

### Ejercicio 5. Supongamos que existe una MT M de tiempo polinomial que, dado un grafo G, devuelve un circuito de Hamilton de G si existe o responde no si no existe. Describir la idea general de una MT M' que, utilizando M, decida en tiempo polinomial si un grafo G tiene un circuito de Hamilton.

Este ejercicio plantea la relación entre un problema de búsqueda (FSAT/Hamiltoniano) y un problema de decisión (SAT/Hamiltoniano). En este caso, se nos da la máquina de búsqueda $M$ y se nos pide construir la de decisión $M'$.

**Idea general de M':**
1. Recibe como entrada el grafo $G$.
2. Invoca a la MT $M$ pasándole el grafo $G$.
3. Si $M(G)$ devuelve un circuito válido (una secuencia de vértices que forma un ciclo hamiltoniano), entonces $M'$ responde **SÍ**.
4. Si $M(G)$ responde "no", entonces $M'$ responde **NO**.

**Complejidad:** Como $M$ es de tiempo polinomial por hipótesis, y la verificación de si el resultado de $M$ es efectivamente un circuito (en caso de que devuelva uno) también es polinomial, la MT $M'$ opera en tiempo polinomial. Esto demuestra que si un problema de búsqueda es tratable, su correspondiente problema de decisión también lo es.
