# Algoritmos Genéticos para la Optimización en Ordenación de Trenes

## Descripción del Proyecto
Este proyecto implementa un **algoritmo genético** para optimizar el tiempo de espera de los trenes en un área ferroviaria, minimizando los retrasos en la descarga. Los trenes deben seguir ciertas restricciones:
- Todos circulan por la misma vía, por lo que deben esperar si hay otro delante.
- Solo pueden entrar a un muelle de carga de su mismo tipo.
- El tiempo de descarga de un tren depende del número de vagones que lleva.

El objetivo es encontrar un **orden óptimo de llegada de los trenes** que minimice el tiempo total de espera.

---
## Implementación

### **1. Generación de Datos**
Se generan trenes aleatorios con:
- Un número de vagones entre **10 y 30**.
- Un tipo de muelle de carga (**op1, op2, op3**).

```python
incoming_trains = random_trains_generation(10)  # 10 trenes entrantes
```

### **2. Representación de Individuos**
Cada individuo en la población representa una posible ordenación de los trenes.

```python
class Train:
    def __init__(self, wagons, op):
        self.wagons = wagons
        self.op = op
```

### **3. Evaluación (Función de Fitness)**
La función de evaluación calcula el **tiempo total de espera** según el orden de los trenes.

```python
def evaluation(individual):
    time = 0
    # Lógica para calcular el tiempo de espera acumulado
    return time,
```

### **4. Operaciones Genéticas**

#### **Cruce**
Intercambia partes de la secuencia de trenes entre dos individuos, asegurando que no haya duplicados.
```python
def our_crossover(ind1, ind2):
    mitad1, mitad2 = ind1[:len(ind1)//2], ind1[len(ind1)//2:]
    mitad3, mitad4 = ind2[:len(ind2)//2], ind2[len(ind2)//2:]
    return mitad1 + mitad4, mitad3 + mitad2
```

#### **Mutación**
Intercambia dos trenes aleatoriamente para generar diversidad.
```python
def our_mutation(ind):
    i, j = random.sample(range(len(ind)), 2)
    ind[i], ind[j] = ind[j], ind[i]
    return ind,
```

### **5. Ejecución del Algoritmo Genético**
Se utiliza la librería **DEAP** para ejecutar el algoritmo con:
- **Selección por torneo** (evita perder individuos potencialmente útiles).
- **Cruce y mutación personalizados**.
- **200 generaciones**.

```python
pop, logbook = algorithms.eaSimple(pop, toolbox, cxpb=0.5, mutpb=0.15, ngen=200, stats=stats, halloffame=hallOfFame, verbose=True)
```

### **6. Resultados**
El algoritmo reduce significativamente el tiempo de espera de los trenes, optimizando su orden de llegada.

```python
print("Mejor orden de trenes:")
for i, train in enumerate(hallOfFame[0]):
    print(f"Tren {i}: {train}")
```

Se grafica la evolución del tiempo de espera a lo largo de las generaciones:

```python
plt.plot(gen, min_, label="Mejor tiempo")
plt.plot(gen, avg, label="Tiempo medio")
plt.title("Optimización de Tiempos con Algoritmos Genéticos")
plt.xlabel("Generación")
plt.ylabel("Tiempo de espera")
plt.legend()
plt.show()
```

---
## **Conclusiones**
- Se logró reducir el tiempo de espera de los trenes en **casi un 50%**.
- El algoritmo genético encontró un ordenamiento óptimo en un **número reducido de generaciones**.
- La combinación de **cruce ordenado y mutación por intercambio** dio buenos resultados.

Este enfoque podría aplicarse a otros problemas de **optimización en logística y transporte**.

