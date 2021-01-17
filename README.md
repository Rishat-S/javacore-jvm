# Задача "Понимание JVM"
## Код для исследования
```java

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
## Описание строк кода:
Класс `JvmComprehension` загружается в область памяти Metaspace.
В момент вызова метода `main` создаётся фрейм(кадр) в Stack Memory.

1. Внутри фрейма `main` создаётся примитив `int i =1`;
2. В области памяти Heap(куча) создаётся объект класса `Object` и ссылка на него `o` передаётся во фрейм метода `main`;
3. Объект `Integer` так же создаётся в Heap, т.к. это класс-обёртка для примитивного типа int. И ссылка на него `ii` записывается во фрейм метода `main`;
4. Вызывается метод `printAll` и во время вызова создаётся фрейм для него в Stack Memory. Параметы указанные в сигнатуре метода(ссылки на объекты и примитивы) копируются в его фрейм в Stack Memory.
5. В Heap создаётся объект типа `Integer` и во фрейм метода `printAll` записывается ссылка на него `uselessVar`;
6. Вызывается метод системного класса `System.out.println` для него создаётся фрейм в Stack Memory, так же создаётся фрейм для метода `o.toString()`, фо фрейм метода `System.out.println` записывается ссылка на объект типа String;
7. Вызывается метод системного класса `System.out.println` для него создаётся фрейм в Stack Memory, и записывается в него ссылка на объект типа String, который создаётся в область памяти Heap.

