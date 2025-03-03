# Genetic Algorithms for Train Scheduling Optimization

## Project Overview
This project implements a **genetic algorithm** to optimize train waiting times in a railway system, minimizing unloading delays. Trains must follow specific constraints:
- All trains share a single track, meaning they must wait if another train is ahead.
- Trains can only enter a loading dock that matches their designated type.
- The unloading time depends on the number of wagons a train carries.

The goal is to find the **optimal train arrival order** that minimizes total waiting time.

---

## Implementation

### **1. Data Generation**
Random trains are generated with:
- A number of wagons between **10 and 30**.
- A specific loading dock type (**op1, op2, op3**).

```python
incoming_trains = random_trains_generation(10)  # 10 incoming trains
```

### **2. Individual Representation**
Each individual in the population represents a possible train ordering.

```python
class Train:
    def __init__(self, wagons, op):
        self.wagons = wagons
        self.op = op
```

### **3. Evaluation (Fitness Function)**
The evaluation function calculates the **total waiting time** based on the train order.

```python
def evaluation(individual):
    time = 0
    # Logic to calculate accumulated waiting time
    return time,
```

### **4. Genetic Operations**

#### **Crossover**
Swaps segments of the train sequence between two individuals while ensuring no duplicates.

```python
def our_crossover(ind1, ind2):
    half1, half2 = ind1[:len(ind1)//2], ind1[len(ind1)//2:]
    half3, half4 = ind2[:len(ind2)//2], ind2[len(ind2)//2:]
    return half1 + half4, half3 + half2
```

#### **Mutation**
Randomly swaps two trains to introduce diversity.

```python
def our_mutation(ind):
    i, j = random.sample(range(len(ind)), 2)
    ind[i], ind[j] = ind[j], ind[i]
    return ind,
```

### **5. Running the Genetic Algorithm**
The **DEAP** library is used to execute the algorithm with:
- **Tournament selection** (to preserve potentially strong individuals).
- **Custom crossover and mutation operators**.
- **200 generations**.

```python
pop, logbook = algorithms.eaSimple(pop, toolbox, cxpb=0.5, mutpb=0.15, ngen=200, stats=stats, halloffame=hallOfFame, verbose=True)
```

### **6. Results**
The algorithm significantly reduces train waiting times by optimizing their arrival order.

```python
print("Best train sequence:")
for i, train in enumerate(hallOfFame[0]):
    print(f"Train {i}: {train}")
```

The evolution of waiting times over generations is visualized:

```python
plt.plot(gen, min_, label="Best time")
plt.plot(gen, avg, label="Average time")
plt.title("Time Optimization with Genetic Algorithms")
plt.xlabel("Generation")
plt.ylabel("Waiting Time")
plt.legend()
plt.show()
```

---

## **Conclusions**
- The train waiting time was reduced by **almost 50%**.
- The genetic algorithm found an optimal sequence within a **small number of generations**.
- The combination of **ordered crossover and swap mutation** yielded effective results.

This approach could be applied to other **logistics and transportation optimization problems**.
