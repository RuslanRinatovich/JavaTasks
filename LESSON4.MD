Предыдущее занятие | &nbsp; | Следующее занятие
:----------------:|:----------:|:----------------:
[Урок 3](Lesson3.md) | [Содержание](readme.md) | [Урок 5](Lesson5.md)

# Задания по теме "Введение в коллекции. HashMap"

# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все три задания.
* Оценка 4 - надо сделать любые два задания.
* Оценка 3 - надо сделать одно любое задание.



# Задание 1

В таблице собраны имена клиентов зоомагазина и сумма, на которую они делали заказы. Посчитайте, сколько всего денег было потрачено на питомцев.

## Заготовка программы

```Java
import java.util.HashMap;

public class Practicum {
    public static void main(String[] args) {
        HashMap<String, Double> orders = new HashMap<>();
        orders.put("Иван И.", 4345.5);
        orders.put("Ольга С.", 76564.43);
        orders.put("Александр Т.", 1234.86);
        orders.put("Александр Р.", 23432.87);
        orders.put("Екатерина О.", 1034753.6);
        orders.put("Ярослав В.", 450.0);

        ... // объявите переменную, где будет сохранена общая сумма
        for (...) { // пройдитесь в цикле по значениям
            ...
        }

        System.out.println("Всего было совершено заказов на сумму: " + ...);
    }
}
```
## Ожидаемый результат работы программы

```Всего было совершено заказов на сумму: 1140781.26```



# Задание 2
Напишите хеш-таблицу государственных праздников stateHolidays, которая будет содержать месяцы и праздничные даты:
- Январь — 1, 7;
- Февраль — 23;
- Март — 8;
- Май — 1, 9;
- Июнь — 12;
- Ноябрь — 4.

## Подсказки
* Импортируйте классы ```HashMap``` и ```ArrayList```.
* Ключи хеш-таблицы ```stateHolidays``` должны быть строкового типа — ```String```, а значения — списки из целых чисел ```ArrayList<Integer>```.
* Создайте для каждого месяца свой список: ```january```, ```february```, ```march```, ```may```, ```june```, ```november```.
* Добавьте в списки элементы с помощью метода ```add()```.
* Добавьте элементы в хеш-таблицу с помощью метода ```put()```.

# Задание 3

В хеш-таблице ```customersOrders``` класса ```OrdersManager``` собрана информация о клиентах зоомагазина (это ключи) и их заказах. Дополните код методов:
* В ```printAllOrders()``` и ```getOrdersSum()```, которые печатают список всех заказов и возвращают их общую сумму, вызовите нужные методы ```HashMap```.
* В методе ```printCustomerOrders(String customerName)``` перед печатью заказов конкретного клиента добавьте проверку наличия его имени в таблице. Это нужно, чтобы избежать ошибки ссылки на ```null```.
* Метод ```getMaxOrderCustomerName()``` должен возвращать имя клиента, который потратил в зоомагазине больше всего. 
Переменные для хранения имени клиента и максимальной суммы заказов мы объявили и инициализировали за вас.
Числовой переменной присвоили 0, а строковой — пустую строку ```""```. Вам нужно дописать логику работы метода. 
Вы уже не раз искали максимум в массивах или списках. Здесь получится очень похоже!
* Метод ```removeUnprofitableOrders``` должен удалять из таблицы клиентов, сумма заказов которых строго меньше 5000.

# Заготовка программы

```Java
public class Practicum {
    public static void main(String[] args) {
        OrdersManager ordersManager = new OrdersManager();

        ordersManager.printAllOrders();
        System.out.println("Всего заказов на сумму: " + ordersManager.getOrdersSum());

        String maxOrderCustomerName = ordersManager.getMaxOrderCustomerName();
        System.out.println("Самая большая сумма заказов у " + maxOrderCustomerName);
        ordersManager.printCustomerOrders(maxOrderCustomerName);

        ordersManager.removeUnprofitableOrders();
    }
}
```
```Java
import java.util.ArrayList;
import java.util.HashMap;

public class OrdersManager {
    HashMap<String, ArrayList<Double>> customersOrders;

    public OrdersManager() {
        customersOrders = new HashMap<>();
        ArrayList<Double> orders = new ArrayList<>();
        orders.add(154.43);
        orders.add(5453.98);
        orders.add(8776.65);
        customersOrders.put("Иван И.", orders);

        orders = new ArrayList<>();
        orders.add(25343.54);
        orders.add(420.50);
        customersOrders.put("Ольга С.", orders);

        orders = new ArrayList<>();
        orders.add(325.90);
        customersOrders.put("Александр Т.", orders);

        orders = new ArrayList<>();
        orders.add(253.54);
        orders.add(420.50);
        customersOrders.put("Александр Р.", orders);

        orders = new ArrayList<>();
        orders.add(780.54);
        orders.add(420.50);
        orders.add(36343.54);
        orders.add(2000.50);
        customersOrders.put("Екатерина О.", orders);
    }

    void printAllOrders() {
        for (String name : ...) { // цикл должен пройтись по ключам
            System.out.println("Заказы " + name + ":");
            ArrayList<Double> value = customersOrders.get(name);
            System.out.println(value);
        }
    }

    double getOrdersSum() {
        double sum = 0;
        for (ArrayList<Double> orders : ...) { // здесь должен быть обход по значениям
            for (double orderPrice : orders) {
                sum += orderPrice;
            }
        }
        return sum;
    }

    void printCustomerOrders(String customerName) {
        if (...) { // проверьте, есть ли указанный ключ в таблице
            System.out.println("Заказы " + customerName + ":");
            System.out.println(customersOrders.get(customerName));
        }
    }

    String getMaxOrderCustomerName() {
        double maxOrder = 0;
        String customerName = "";

        ... // допишите логику работы метода

        return customerName;
    }

    void removeUnprofitableOrders() {
        ArrayList<String> names ... // создайте список клиентов с заказами меньше 5000
        
        // наполните список names
        for ...

            double ordersSum = 0;
            for ...

            if (ordersSum < 5000) {
                ...
            }
        }

        for ... // удалите из хеш-таблицы тех, чьи расходы строго меньше 5000
           
            System.out.println("Клиента " + name + " больше нет в таблице.");
        }
    }
}
```
### Ожидаемый результат работы программы

 ```
 Заказы Александр Т.:
[325.9]
Заказы Александр Р.:
[253.54, 420.5]
Заказы Иван И.:
[154.43, 5453.98, 8776.65]
Заказы Екатерина О.:
[780.54, 420.5, 36343.54, 2000.5]
Заказы Ольга С.:
[25343.54, 420.5]
Всего заказов на сумму: 80694.12
Самая большая сумма заказов у Екатерина О.
Заказы Екатерина О.:
[780.54, 420.5, 36343.54, 2000.5]
Клиента Александр Т. больше нет в таблице.
Клиента Александр Р. больше нет в таблице.
 ```

### Подсказки

* Для получения ключей из таблицы вам понадобится метод ```keySet()```.
* Для получения всех значений в таблице используйте метод ```values()```.
* Для проверки имени клиента воспользуйтесь методом ```containsKey(customerName)`.
* Чтобы найти клиента с наибольшей суммой заказов, пройдите по всем клиентам 
и посчитайте их суммы заказов — это можно сделать с помощью вложенных циклов ```for```. 
Внутри второго цикла сравнивайте суммы заказов и сохраняйте наибольшую и имя клиента. 
Так вы получите искомый результат.
* Чтобы найти клиентов, чьи заказы меньше 5000, пройдите по ключам таблицы с помощью цикла 
```for: for (String name : customersOrders.keySet())```. Затем получите сумму заказа. Проверьте её с помощью ```if``` .
* С помощью ещё одного ```for``` пройдите по полученному списку с именами клиентов, 
чьи заказы меньше 5000 (```for (String name : names)```), и через метод ```remove``` удалите их из таблицы.


Предыдущее занятие | &nbsp; | Следующее занятие
:----------------:|:----------:|:----------------:
[Урок 3](Lesson3.md) | [Содержание](readme.md) | [Урок 5](Lesson5.md)