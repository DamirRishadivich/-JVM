# Визуализация информации по теме "JVM. организация памяти, сборщик мусора, VisualVM"
Пример кода:
```java
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

## main() - первый фрейм
*В момент вызова создается фрейм в стеке (Stack Memory)*

### int i = 1;
Т.к int относится к примитивным типам данных, то он создается и инициализируется в стеке, внутри своего фрейма.

## Object o = new Object();
new Object - резервирует себе место в куче (heap). o типа Object - инициализируется в своем фрейме и хранит ссылку на область памяти в куче.

## Integer ii = 2;
Integer относится к ссылочным типам. Будет создан и инициализирован в стеке, но будет указывать на объект памяти в куче.

## printAll(o, i, ii); - второй фрейм
Вызывается  метод printAll.В стеке создается новый фрейм. 
## private static void printAll(Object o, int i, Integer ii) {
Object o - уже есть в куче. Создается ссылочная переменная o, которая указывает на тот же объект в куче, что и до этого.

int i - создается в стеке, внутри фрейма printAll.

Integer i  - уже есть в куче. Создается ссылочная переменная o, которая указывает на тот же объект в куче, что и до этого.

## Integer uselessVar = 700;
Ссылочная переменная uselessVar создается в стеке, но будет указывать на объект в куче.

## System.out.println(o.toString() + i + ii);
Т.к есть toString, то параметры sout'a приводятся к String. В куче резервируется объект этой строки. sout обращается к нему из стека, своего фрейма

## System.out.println("finished");
Грубо говоря предварительно создается String = "finished". sout срабатывает в стеке, вызывая из кучи эту строку.
