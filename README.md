
### Prioridades en Java

En Java, el concepto de "prioridades" se utiliza en varios contextos, pero uno de los más comunes es en el manejo de **hilos (Threads)**. Cada hilo en Java tiene una prioridad asignada que influye en la manera en que el planificador de hilos del sistema operativo decide cuál ejecutar.

#### **Cómo funcionan las prioridades en los hilos**
La clase `Thread` en Java proporciona un mecanismo para establecer y obtener la prioridad de un hilo mediante los métodos:
- `setPriority(int priority)`: Establece la prioridad del hilo.
- `getPriority()`: Devuelve la prioridad actual del hilo.

Las prioridades de los hilos son valores enteros que oscilan entre:
- `Thread.MIN_PRIORITY` (valor 1): Menor prioridad.
- `Thread.NORM_PRIORITY` (valor 5): Prioridad normal (valor predeterminado).
- `Thread.MAX_PRIORITY` (valor 10): Mayor prioridad.

Un hilo con mayor prioridad **tiene más probabilidades** de ejecutarse antes que otro con una prioridad más baja, aunque no se garantiza debido a la implementación del planificador subyacente (que depende del sistema operativo).

#### **Ejemplo de uso**
```java
public class PriorityExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            System.out.println("Hilo 1 ejecutándose.");
        });
        Thread t2 = new Thread(() -> {
            System.out.println("Hilo 2 ejecutándose.");
        });

        // Establecer prioridades
        t1.setPriority(Thread.MIN_PRIORITY);
        t2.setPriority(Thread.MAX_PRIORITY);

        // Iniciar hilos
        t1.start();
        t2.start();
    }
}
```
En este ejemplo, aunque `t2` tiene una mayor prioridad, no hay garantía de que siempre se ejecute antes que `t1`, ya que esto depende del planificador de hilos.

#### **Consideraciones importantes**
1. **No es determinista**: La prioridad es solo una sugerencia para el planificador. Factores como la carga del sistema operativo y la implementación del planificador influyen en la ejecución.
2. **No abuse de las prioridades**: Depender demasiado de las prioridades puede conducir a aplicaciones no portables y difíciles de depurar.
3. **Uso recomendado**: Utilice prioridades para tareas críticas, pero combine esto con técnicas como la sincronización y el control de concurrencia para un diseño más robusto.

#### **Otras áreas donde se usan prioridades**
Además de los hilos, las prioridades también se aplican en estructuras de datos como las **colas de prioridad (`PriorityQueue`)**, que ordenan elementos según su prioridad definida.

#### **Conclusión**
Las prioridades en Java son una herramienta útil para gestionar el comportamiento de los hilos y optimizar procesos. Sin embargo, su efectividad depende del contexto y de las garantías que ofrece el sistema operativo subyacente.
