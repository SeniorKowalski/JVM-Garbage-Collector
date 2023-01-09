# JVM-Организация памяти-Garbage-Collector

```Java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```
1. Создаётся фрейм метода main и в него записывается int i = 1.
2. В Heap создаётся объект "о" и ссылка на него помещается в stack memory фрейма метода main.
3. В Heap создаётся объект класса Integer со значением 2 и ссылка на него помещается в stack memory фрейма метода main.
4. Создаётся фрейм метода printAll, в его stack memory помещаются ссылки на объекты "о", "ii" и значение примитива "i"(1).
5. В Heap создаётся объект класса Integer со значением 700 и ссылка на него помещается в stack memory фрейма метода printAll.
6. Создаётся фрейм метода printAll, в его stack memory помещается ссылка на фрейм метода printAll.
7. Создаётся фрейм метода println, в его stack memory помещается объект из пула строк кучи, состоящий из массива байт, представляющих собой строку "finished".

## Class loader
Загрузчики классов делегируют запросы загрузчику-родителю начиная с Bootstrap class loader, далее переходя к Platform class loader а затем к Application class loader.
* **Bootstrap class loader** является базовым и загружает классы из bootstrap classpath.
* **Platform class loader** загружает модули Java SE и JDK. 
* **Application class loader** используется для загрузки классов приложения из classpath.

Таким образом, в данном случае, для загрузки класса JvmComprehension используется Application class loader. 

## Garbage collector 
В данном случае осуществляет сборку мусора при завершении работы программы, так как памяти достаточно, чтобы не делать этого во время выполнения.
