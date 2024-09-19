# Задания по теме "Инкапсуляция"

# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все три задания.
* Оценка 4 - надо сделать любые два задания.
* Оценка 3 - надо сделать одно любое задание.



# Задание 1
Коллега помогал главному бухгалтеру и написал калькулятор рабочих часов,
но не доделал работу и ушёл в отпуск. Сотрудники компании рискуют остаться 
без выплат! Доработайте приложение и расставьте модификаторы доступа 
в соответствии с логикой приложения.  
Доступ к рабочим часам и имени работника нужно закрыть, 
чтобы уберечь эти данные. А вот доступ к повышающему коэффициенту 
можно сделать максимально широким. Чтобы избежать ошибок при компиляции, 
конструктор класса WorkCalculator тоже лучше сделать доступным. Кроме того,
нужно предусмотреть публичный доступ к интерфейсу калькулятора — всем его методам.

## Заготовка программы

#### Класс WorkCalculator
```Java
package ru.yandex.practicum.work;

public class WorkCalculator {
    
    public int workingHours = 8; 
    String workerName;  
    private double coefficient; 

    WorkCalculator(String newName) {
        workerName = newName;
    }

    private String getWorkerName() {
        return workerName;
    }

    int calculate(int workDays) {
        return workDays * workingHours; 
    }

    double calculateWithCoefficient(int workDays) {
        return workDays * workingHours * coefficient;
    }
}
```

#### Класс Main
```Java
package ru.yandex.practicum;

import ru.yandex.practicum.work.WorkCalculator;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите имя работника:");
        WorkCalculator calculator = new WorkCalculator(scanner.next());

        System.out.println("Введите коэффициент в формате 1.5:");
        calculator.coefficient = scanner.nextDouble();

        System.out.println("Введите количество отработанных дней без коэффициента:");
        double hoursWithoutCoefficient = calculator.calculate(scanner.nextInt());

        System.out.println("Введите количество отработанных дней с коэффициентом:");
        double hoursWithCoefficient = calculator.calculateWithCoefficient(scanner.nextInt());
        
        double allWorkHours = hoursWithoutCoefficient + hoursWithCoefficient;
        // метод printf позволяет нам вывести строку с форматированием
        // символ %s заменит строку, а %.2f число с 2 знаками после запятой
        System.out.printf("Работник %s отработал %.2f часов.",
        calculator.getWorkerName(), allWorkHours);
    }
}
```

### Подсказки

* Переменные ```workingHours``` и workerName должны иметь модификатор доступа ```private```.
* Для переменной ```coefficient``` и конструктора ```WorkCalculator(String newName)``` нужен доступ ```public```.
* С модификатором ```private``` не получится получить доступ к методу ```getWorkerName()``` — нужен ```public```.
* Для успешной компиляции у методов ```calculate()``` и ```calculateWithCoefficient()``` нужно заменить модификатор по умолчанию на ```public```.


# Задание 2
Напишите программу для бронирования комнаты с завтраком
в мини-отеле “Royal Java Bed and Breakfast”.
В нём 10 номеров. 
Реализуйте методы для заселения ```book()``` и 
выезда ```free()``` гостей. 
Расставьте нужные модификаторы доступа: 
переменные ```capacity``` (вместимость) и ```full``` (заполненность),
а также метод ```printRooms()``` нужно скрыть — доступ
к ним должен остаться только внутри класса ```BedAndBreakfast```.
Сам класс ```BedAndBreakfast``` и другие методы в нём должны иметь 
максимальный уровень доступа. Не забудьте,
что когда вы закроете переменные,
к ним нельзя будет обратиться — нужно будет обращаться 
к методам.

#### Класс BookingService
```Java
package ru.yandex.practicum.booking;

... // импортируйте классы BedAndBreakfast и Scanner

public class BookingService {

    public static void main(String[] args) {
        // можно забронировать одну из комнат
        BedAndBreakfast hotel = new BedAndBreakfast();
        Scanner scanner = new Scanner(System.in);

        /* Обратите внимание, здесь для удобства мы используем  
        другую конструкцию для оформления цифрового меню.*/ 
 
        while (true) {
            System.out.println("Что вы хотите сделать?");
            System.out.println("1 - Забронировать номер");
            System.out.println("2 - Освободить номер");
            System.out.println("3 - Проверить наличие свободных номеров");
            System.out.println("0 — Выход");

            int command = scanner.nextInt();
            /* switch-case конструкция заменяет if-else условия,
            код получается компактнее и быстрее читается */
            switch (command) {
                case 1:
                    // используется публичный метод
                    hotel.book();
                    // break позволяет выйти из условия, иначе - идём дальше
                    break;
                case 2:
                    hotel.free();
                    break;
                case 3:
                    if (hotel.full) { 
                        System.out.println("Больше нет мест¯\\_(ツ)_/¯");
                    } else {
                        System.out.println("Есть свободные номера!");
                    }
                    break;
                case 0:
                    System.out.println("Выход");
                    
                    /* Метод exit() останавливает работу JVM, завершая программу.
                    В качестве аргумента принимает число — код ошибки.
                    Если оно не равно 0 — программа завершилась некорректно.*/
                    System.exit(0); // код равен 0, программа была завершена намеренно
                    // break в этом случае не нужен
                default:
                    System.out.println("Извините, такой команды пока нет.");
                    break;
            }
        }
    }
}
```

#### Класс BedAndBreakfast
```Java
package ru.yandex.practicum.model;

class BedAndBreakfast { // сделайте класс общедоступным

    ... // число свободных номеров (10) сохраните в переменную capacity

    ... // сохраните в переменную full значение false - есть номера в наличии

    void book() { // метод для бронирования комнат
        if (...) { // если есть свободные номера
            System.out.println("Забронирован ещё один номер!");
            ... // уменьшите количество свободных номеров на один
            printRooms();
            if (capacity == 0) {
                full = true;
            }
        } else {
            System.out.println("Свободных номеров нет!");
        }
    }

    void printRooms() {
        System.out.println("Свободных номеров - " + ...);
    }

    void free() { // метод для освобождения комнат
        if (...) { // если свободных комнат меньше 10
            ... // увеличиваем количество свободных мест на одно
            System.out.println("Освободился номер!");
            printRooms();
            full = false;
        } else {
            System.out.println("В гостинице только 10 номеров.");
        }
    }

     boolean isFull() {
        return full;
    }
}
```

### Подсказки

* Чтобы импортировать классы ```BedAndBreakfast``` и ```Scanner``` нужно ключевое слово ```import``` и имена пакетов: ```ru.yandex.practicum.model``` и ```java.util```.
* Класс ```BedAndBreakfast```, методы ```book()```, ```free()```, ```isFull()``` должны иметь модификатор ```public```. Переменные ```int capacity``` и ```boolean full```, метод ```printRooms()```, модификатор ```private```.
* Проверить, есть ли свободные номера в методе ```book()```, нужно с помощью отрицания — !full.
* Количество свободных номеров в методе ```free()``` должно быть строго меньше 10 — ```capacity < 10```.
* Для увеличения и уменьшения числа номеров в методах используйте инкремент и декремент: ```capacity++``` и ```capacity--```.
* В ```case 3``` нужно заменить вызов переменной ```hotel.full``` (она стала ```private```) на вызов метода ```hotel.isFull()``` — он теперь ```public```.


# Задание 3

Вам нужно снять наличные в банкомате, 
но он сломался и выводит только консоль с недописанным кодом.
По счастливой случайности — на Java. 
Допишите код — реализуйте методы в классе ```BankAccount```. 
Чтобы установить и считать значение суммы денег на счёте
```moneyAmount```, вам понадобятся get- и set-методы. 
Чтобы снять деньги со счёта и обнулить его — метод ```withdrawAll()```,
который должен обнулять счёт и печатать количество выданных денег
в формате: Со счёта снято 1000 р. 
Все методы должны иметь самый широкий уровень доступа.
В результате запуска программы в консоли должно появиться:
 ```
Количество денег на счету - 1000 р. (сумма может быть любой)
Со счёта снято 1000 р.
Количество денег на счету - 0 р.
 ```

# Заготовка программы

```Java
public class Practicum {
    public static void main(String[] args) {
        BankAccount bankAccount = new BankAccount();
        ... // передайте в банкомат сумму на счету
        System.out.println("Количество денег на счету - " + ... + " р.");
        ... // вызовите метод вывода средств
        System.out.println("Количество денег на счету - " + ... + " р.");
    }
}

class BankAccount {
    private long moneyAmount;

    // допишите код методов
    // используйте параметр newMoneyAmount для установки нового значения
}
```
### Подсказки

* Метод ```getMoneyAmount()``` должен возвращать значение 
переменной ```moneyAmount```. 
Тип возвращаемого значение будет совпадать с типом переменной.
* Метод ```setMoneyAmount()``` должен принимать
в качестве аргумента значение суммы на
счету ```newMoneyAmount``` и сохранять его в поле ```moneyAmount```.
* Передать в ```moneyAmount``` сумму (например, 1000) 
нужно через вызов метода ```setMoneyAmount(1000)``` в классе ```Practicum```.
* Получить значение ```moneyAmount``` до и после 
обнуления нужно через вызов метода ```getMoneyAmount()```.