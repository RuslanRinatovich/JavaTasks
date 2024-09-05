# Задания по теме "Сложные типы данных: продолжение"


# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все три задания.
* Оценка 4 - надо сделать любые два задания.
* Оценка 3 - надо сделать одно любое задание.

# Задание 1

Часто при обновлении программ нужно поддерживать старый код. Доработайте код новой версии игры-стратегии, чтобы он поддерживал параметры из старой версии:
* Поле ```gold``` типа ```long``` необходимо сохранить в переменную ```characterGold``` типа ```int``` (точно известно, что значение параметра ```gold``` меньше 
2 000 000 000).
* Поле ```silver``` типа ```byte``` необходимо сохранить как переменную ```characterSilver``` типа ```int```, предварительно умножив её на 
100.
* Поле ```wood``` типа ```short``` необходимо сохранить как переменную ```characterWood``` типа ```double```.
* Поле ```health``` типа ```long``` необходимо сохранить как переменную ```characterHealth``` типа ```byte``` (точно известно, что значение параметра ```health``` меньше 
100).
* Поле ```hasHelper``` типа boolean необходимо сохранить как переменную characterHelpersNumber типа byte. Если параметр hasHelper равен true, то в переменную ```characterHelpersNumber``` сохранить единицу, если ```false``` — ноль.

## Заготовка для приложения
```java
public class Main {
    public static void main(String[] args) {
        long inputGold = 200L;
        byte inputSilver = 39;
        short inputWood = 2005;
        long inputHealth = 97L;
        boolean inputHasHelper = true;

        Resources characterResources = new Resources(
                inputGold,
                inputSilver,
                inputWood,
                inputHealth,
                inputHasHelper
        );

        int characterGold = ...
        int characterSilver = ...
        double characterWood = ...
        byte characterHealth = ...
        byte characterHelpersNumber;

        // установка значения characterHelpersNumber в зависимости от значения hasHelper
        ...

        Character character = new Character(
                characterGold,
                characterSilver,
                characterWood,
                characterHealth,
                characterHelpersNumber
        );

        System.out.println("Персонаж создан успешно!");
        System.out.println("Количество золота: " + character.gold);
        System.out.println("Количество серебра: " + character.silver);
        System.out.println("Количество дерева: " + character.wood);
        System.out.println("Здоровье: " + character.health);
        System.out.println("Количество помощников: " + character.helpersNumber);
        System.out.println("Навстречу приключениям!");
    }
}
```

```java
class Resources {
    long gold;
    byte silver;
    short wood;
    long health;
    boolean hasHelper;

    public Resources(
            long inputGold,
            byte inputSilver,
            short inputWood,
            long inputHealth,
            boolean inputHasHelper
    ) {
        gold = inputGold;
        silver = inputSilver;
        wood = inputWood;
        health = inputHealth;
        hasHelper = inputHasHelper;
    }
}
```

```java
class Character {
    int gold;
    int silver;
    double wood;
    byte health;
    byte helpersNumber;

    public Character(
            int characterGold,
            int characterSilver,
            double characterWood,
            byte characterHealth,
            byte characterHelpersNumber
    ) {
        gold = characterGold;
        silver = characterSilver;
        wood = characterWood;
        health = characterHealth;
        helpersNumber = characterHelpersNumber;
    }
}
```

## Подсказки


* Обращаться к параметрам класса ```Resources``` необходимо через ```characterResources.{параметр}```.
* Чтобы привести ```long``` ```characterResources.gold``` к типу ```int```, нужно использовать явное приведение типов через ```(int)```.
*  ```characterResources.silver``` имеет тип ```byte```, а ```characterSilver``` — тип ```int```. Java сама приведёт данные к нужному типу благодаря неявному расширению.
*  ```characterResources.wood``` имеет тип ```short```, а ```characterWood``` — тип ```double```. Здесь Java сама приведёт данные к нужному типу благодаря неявному расширению.
* Чтобы привести ```long``` ```characterResources.health``` к типу ```byte```, нужно использовать явное приведение типов через (byte).
* ```boolean``` нельзя привести к типу ```byte``` с помощью приведения типов, необходимо использовать ```if```.

## Ожидаемый результат работы программы


```
Персонаж создан успешно!
Количество золота: 200
Количество серебра: 3900
Количество дерева: 2005.0
Здоровье: 97
Количество помощников: 1
Навстречу приключениям!
```


# Задание 2


Прочитайте код приложения онлайн-банка, в котором пользователь может по желанию завести счета в трёх валютах. В программу забрался баг — вне зависимости от выбора пользователя сразу открываются все три счёта. 
С помощью классов-обёрток и их свойств исправьте код так, чтобы открывались счета только в тех валютах, которые выберет пользователь. Счета необходимо создавать с нулевым балансом.


```java


import java.util.Scanner;

public class Practicum {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите имя пользователя:");
        String name = scanner.nextLine();
        PersonAccount user = new PersonAccount(name);

        System.out.println("Хотите открыть счёт в RUB?");
        System.out.println("1 - Да");
        System.out.println("2 - Нет");
        int command = scanner.nextInt(); 
        if (command == 1) {
            user.moneyRUB = 0.0;
        }

        System.out.println("Хотите открыть счёт в USD?");
        System.out.println("1 - Да");
        System.out.println("2 - Нет");
        command = scanner.nextInt();
        if (command == 1) {
            user.moneyUSD = 0.0;
        }

        System.out.println("Хотите открыть счёт в EUR?");
        System.out.println("1 - Да");
        System.out.println("2 - Нет");
        command = scanner.nextInt();
        if (command == 1) {
            user.moneyEUR = 0.0;
        }

        System.out.println("Поздравляем, аккаунт для пользователя " + user.name + " создан.");
        System.out.println("Открытые счета:");
        if (user.moneyRUB == 0.0) {
            System.out.println("- RUB");
        }
        if (user.moneyUSD == 0.0) {
            System.out.println("- USD");
        }
        if (user.moneyEUR == 0.0) {
            System.out.println("- EUR");
        }
        
    }
}

class PersonAccount {
    String name;      // имя и фамилия
    double moneyRUB;  // счёт в рублях
    double moneyUSD;  // счёт в долларах
    double moneyEUR;  // счёт в евро
    

    PersonAccount(String userName) {
        name = userName;
    }
}
```

# Задача 3


Кота Пикселя на вечер субботы оставили бабушке. Она приготовила ему на выбор говядину и курицу, а перед сном налила молока и поставила блюдце сливок. Пиксель внимательно следит за питанием и в обоих случаях выбрал наименее калорийную еду. Вычислите, сколько всего ккал съел Пиксель за день, и проверьте, уложился ли питомец в свой лимит в 
100 ккал. Чтобы код сработал, вам также нужно найти и исправить ошибки, касающиеся типов.

```java
public class Practicum {
    public static void main(String[] args) {
        String pixelKcalDay = "43"; // столько калорий съел Пиксель до похода к бабушке
        String beefKcal = "30.2"; // калорийность говядины
        String chickenKcal = "23.8"; // калорийность курицы
        String creamKcal = "32.1"; // калорийность сливок
        String milkKcal = "13.5"; // калорийность молока

        float pixelChoice = getMinKcalsSum(beefKcal, chickenKcal, creamKcal, milkKcal);
        float totalKcal = int.parseInt(pixelKcalDay) + pixelChoice;
        checkKcal(totalKcal);
    }

    private static Float getMinKcalsSum(String firstDishKcal, String secondDishKcal, String firstDesert, String secondDesert) {
        float minDishKcal = ... // вычислите минимальную калорийность основного блюда
        float minDesertKcal = ... // вычислите минимальную калорийность десерта
        return minDishKcal + minDesertKcal;
    }

    private static void checkKcal(float catKcal) {
        if (catKcal == null) {
            System.out.println("Что-то пошло не так");
        } else {
            System.out.println("Калорийность рациона Пикселя за день: " + catKcal);
            if (catKcal > 100) {
                System.out.println("Пиксель сегодня не уложился в норму.");
            } else {
                System.out.println("Лимит не превышен!");
            }
        }
    }
}
```

## Подсказки


* Метод ```parse``` есть только у ссылочных типов. Преобразование из строки в число калорийности рациона Пикселя до похода к бабушке будет таким — ```Integer.parseInt(pixelKcalDay)```.
* Методы по нахождению наименьшего из двух значений есть только у классов-обёрток — вам нужен ```Float.min()```.
* Чтобы найти наименьшее от двух значений типа ```float```, нужно привести к этим типам переменные типа ```String``` с помощью метода ```parse```. Например: ```Float.parseFloat(firstDishKcal)```.
* В методе ```checkKcal``` параметр ```catKcal``` должен иметь тип ```Float```, а не ```float```. У примитива в отличие от класса-обёртки не может быть значение ```null```.

## Ожидаемый результат работы программы

```
Калорийность рациона Пикселя за день: 80.3
Лимит не превышен!
```