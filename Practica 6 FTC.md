# Resolución Trabajo Práctico Nro 6 - FTC

## Ejercicio 1. Responder breve y claramente:

### a. Dar un esquema de prueba de la transitividad de las reducciones polinomiales.
Si tenemos tres lenguajes $L_1, L_2, L_3$ tales que $L_1 \le_p L_2$ y $L_2 \le_p L_3$, entonces existe una reducción polinomial $f$ de $L_1$ a $L_2$ y una reducción polinomial $g$ de $L_2$ a $L_3$.
La función compuesta $h(w) = g(f(w))$ es una reducción de $L_1$ a $L_3$:
1. **Correctitud**: $w \in L_1 \iff f(w) \in L_2 \iff g(f(w)) \in L_3$.
2. **Complejidad**: Como $f$ es computable en tiempo $poly_1(|w|)$ y produce una salida de tamaño a lo sumo $poly_1(|w|)$, y $g$ es computable en tiempo $poly_2(|f(w)|)$, la composición se computa en tiempo $poly_2(poly_1(|w|))$, lo cual sigue siendo polinomial.

### b. ¿Cuándo un lenguaje es NP-difícil y cuándo es NP-completo?
*   **NP-difícil (NP-hard)**: Un lenguaje $L$ es NP-difícil si **todo** lenguaje $L' \in NP$ se reduce polinomialmente a él ($L' \le_p L$). No se requiere que $L$ pertenezca a NP.
*   **NP-completo (NPC)**: Un lenguaje $L$ es NP-completo si cumple dos condiciones:
    1. $L \in NP$.
    2. $L$ es NP-difícil.

### c. ¿Por qué si $P \neq NP$, un lenguaje NP-completo no pertenece a $P$?
Por el teorema visto en clase: si $L \in NPC$ y $L \in P$, entonces $P = NP$. Esto se debe a que, por definición de NPC, cualquier lenguaje en $NP$ se reduce a $L$. Si $L$ se puede decidir en tiempo polinomial, entonces todos los lenguajes de $NP$ también (usando la reducción y luego el decisor de $L$).
Por el contrarrecíproco, si $P \neq NP$, entonces ningún lenguaje NP-completo puede estar en $P$.

### d. Enunciar el esquema visto en clase para agregar un lenguaje a la clase NPC.
Para demostrar que un nuevo lenguaje $L$ es NP-completo:
1.  **Probar que $L \in NP$**: Mostrar que existe un verificador polinomial para $L$.
2.  **Probar que $L$ es NP-difícil**: Seleccionar un lenguaje $L'$ que ya se sepa que es NP-completo (por ejemplo, SAT o 3-SAT) y construir una reducción polinomial $L' \le_p L$.

### e. ¿Cuándo se sospecha que un lenguaje de NP está en NPI?
Se sospecha que un lenguaje pertenece a la clase **NPI** (NP-Intermediate) cuando:
1. El lenguaje está en $NP$.
2. No se conoce un algoritmo de tiempo polinomial para decidirlo ($L \notin P$).
3. No se ha logrado encontrar una reducción desde un lenguaje NP-completo hacia él ($L \notin NPC$).
Ejemplos clásicos mencionados en clase son el Isomorfismo de Grafos (ISO) y la Factorización de Enteros (FACT).

---

## Ejercicio 2. Probar:

### a. Si $L_1 \in NPC$ y $L_2 \in NPC$, entonces $L_1 \le_p L_2$ y $L_2 \le_p L_1$.
*   Como $L_1 \in NPC$, por definición es NP-difícil, lo que significa que **todo** lenguaje en $NP$ se reduce a él. Dado que $L_2 \in NPC$, sabemos que $L_2 \in NP$. Por lo tanto, $L_2 \le_p L_1$.
*   Análogamente, como $L_2 \in NPC$, es NP-difícil. Como $L_1 \in NP$, entonces $L_1 \le_p L_2$.

### b. Si $L_1 \le_p L_2, L_2 \le_p L_1$ y $L_1 \in NPC$, entonces $L_2 \in NPC$.
Debemos verificar las dos condiciones de NPC para $L_2$:
1.  **$L_2 \in NP$**: Como $L_1 \in NPC$, entonces $L_1 \in NP$. Dado que $L_2 \le_p L_1$ y $NP$ es cerrado bajo reducciones polinomiales hacia atrás (si se reduce a algo en NP, está en NP), entonces $L_2 \in NP$.
2.  **$L_2$ es NP-difícil**: Como $L_1 \in NPC$, sabemos que para todo $L' \in NP, L' \le_p L_1$. Como nos dan que $L_1 \le_p L_2$, por la propiedad de transitividad (Ejercicio 1a), tenemos que para todo $L' \in NP, L' \le_p L_2$.
Al cumplir ambas, $L_2 \in NPC$.

---

## Ejercicio 3. Probar que $SAT^c$ es CO-NP-completo.
Un lenguaje $L$ es CO-NP-completo si $L \in CO-NP$ y todo lenguaje de $CO-NP$ se reduce a él.
1.  **$SAT^c \in CO-NP$**: Por definición, $CO-NP$ contiene a los complementos de los lenguajes en $NP$. Como $SAT \in NP$, su complemento $SAT^c$ está en $CO-NP$.
2.  **Reducción**: Sea $L'$ cualquier lenguaje en $CO-NP$. Entonces su complemento $L'^c$ está en $NP$.
    Como $SAT \in NPC$, existe una reducción polinomial $f$ tal que $L'^c \le_p SAT$.
    Utilizando la ayuda: $L_1 \le_p L_2 \iff L_1^c \le_p L_2^c$.
    Entonces, $(L'^c)^c \le_p SAT^c$, lo que equivale a $L' \le_p SAT^c$.
Por lo tanto, $SAT^c$ es CO-NP-completo.

---

## Ejercicio 4. Sean $A, B$ tales que $A \neq \emptyset, A \neq \Sigma^*$ y $B \in P$. Probar $(A \cap B) \le_p A$.
Para que exista la reducción $f: \Sigma^* \to \Sigma^*$, debe cumplirse $w \in (A \cap B) \iff f(w) \in A$.
Como $A \neq \emptyset$ y $A \neq \Sigma^*$, existen constantes $a_{in} \in A$ y $a_{out} \notin A$.
Definimos la función $f(w)$ de la siguiente manera:
1. Si $w \in B$:
   Retornar $w$.
2. Si $w \notin B$:
   Retornar $a_{out}$.

**Análisis de Correctitud**:
* Si $w \in (A \cap B)$: Entonces $w \in B$ y $w \in A$. Por definición, $f(w) = w$, y como $w \in A$, la condición se cumple.
* Si $w \notin (A \cap B)$:
    - Caso 1: $w \in B$ pero $w \notin A$. Entonces $f(w) = w$, y como $w \notin A$, se cumple.
    - Caso 2: $w \notin B$. Entonces $f(w) = a_{out}$, y por definición $a_{out} \notin A$, se cumple.

**Complejidad**: Como $B \in P$, chequear si $w \in B$ toma tiempo polinomial. El resto de las operaciones son constantes. Por lo tanto, $f$ es una reducción polinomial.

---

## Ejercicio 5. Probar que $SH-s-t$ es NP-completo.
$SH-s-t = \{(G, s, t) \mid G$ tiene un camino de Hamilton de $s$ a $t\}$.

### 1. $SH-s-t \in NP$
Dado un certificado (una secuencia de vértices), un verificador puede en tiempo polinomial:
- Verificar que todos los vértices del grafo aparecen exactamente una vez.
- Verificar que el primer vértice es $s$ y el último es $t$.
- Verificar que cada par adyacente en la secuencia tiene una arista en $G$.

### 2. $SH-s-t$ es NP-difícil (Reducción $CH \le_p SH-s-t$)
Sabemos que el problema del Circuito Hamiltoniano ($CH$) es NP-completo.
Dada una instancia de $CH$, un grafo $G = (V, E)$:
1. Elegimos un vértice arbitrario $v \in V$.
2. Construimos un nuevo grafo $G'$ reemplazando $v$ por dos nuevos vértices: $s$ (inicio) y $t$ (fin).
3. Para cada arista $(v, u) \in E$ en el grafo original, agregamos las aristas $(s, u)$ y $(t, u)$ en $G'$.
4. Los demás vértices y aristas de $G$ se mantienen igual en $G'$.

**Correctitud**:
* Si $G$ tiene un **Circuito Hamiltoniano**, este debe pasar por $v$. Sea el circuito $v \to v_1 \to v_2 \dots \to v_k \to v$. En $G'$, esto se convierte en el camino $s \to v_1 \to v_2 \dots \to v_k \to t$, que es un **Camino de Hamilton de $s$ a $t$**.
* Si $G'$ tiene un **Camino de Hamilton de $s$ a $t$**, este visita todos los nodos una vez. Como $s$ y $t$ tienen los mismos vecinos que $v$ en el grafo original, al "unirlos" nuevamente en $v$ obtenemos un ciclo que visita todos los nodos de $G$ exactamente una vez: un **Circuito Hamiltoniano**.

Como la transformación del grafo es polinomial, queda demostrada la NP-completitud.
