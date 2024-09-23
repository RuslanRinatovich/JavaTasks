# Задания по теме "Наследование"

# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все три задания.
* Оценка 4 - надо сделать любые два задания.
* Оценка 3 - надо сделать одно любое задание.



# Задание 1
Прочитайте код и решите задачку: у трёх сыновей один родитель, у одного родителя — один сын, а один сын — сам родитель. Затем исправьте код таким образом, чтобы он сработал и в консоли было напечатано:

```
Рисуем круг
Рисуем квадрат
Рисуем прямоугольник
Рисуем круг
Превращаем круг в овал 
```
Новые методы в классах создавать нельзя.

## Заготовка программы

#### Класс **Practicum**
```Java
public class Practicum {
    public static void main(String[] args) {
        ...
        circle.drawCircle();
        square.drawSquare();
        rectangle.drawRectangle();
        ellipse.drawCircle();
        ellipse.circleToEllipse();
    }
}

class Figure {
    public void drawCircle() {
        System.out.println("Рисуем круг");
    }

    public void drawSquare() {
        System.out.println("Рисуем квадрат");
    }

    public void drawRectangle() {
        System.out.println("Рисуем прямоугольник");
    }
}

class Circle {
}

class Square {
}

class Rectangle {
}

class Ellipse {
    public void circleToEllipse() {
        System.out.println("Превращаем круг в овал");
    }
}
```


# Задание 2
На заводе скоростных автомобилей “Texla” построили новую модель “Q”. Перед выходом на рынок её необходимо протестировать. Но с программой для тестирования что-то не так — в ней смешались классы из двух разных проектов и пропали все наследственные связи. Вам нужно отсеять лишние классы и восстановить цепочку наследования. После того как это будет сделано, проверьте модификаторы — везде ли обеспечен необходимый уровень доступа!

#### Класс Practicum
```Java
class Practicum {
    public static void main(String[] args) {
        ModelQ testCar = new ModelQ();

        System.out.println("Характеристики модели:");
        System.out.println("Ускорение: " + testCar.acceleration + " км/(ч*с)");
        System.out.println("Максимальная скорость: " + testCar.maxSpeed + " км/ч");
        // Символ \n позволяет оставлять пустую строку в консоли
        System.out.println("\nНачало теста!");
        System.out.println("Количество колёс: " + testCar.wheelsNumber);

        testCar.turnTo("Север");
        System.out.println("Направление: " + testCar.direction);
        System.out.println("Едем на автопилоте:");
        for (int second = 0; second < 5; second++) {
            testCar.accelerateByAutopilot();
        }
        System.out.println("Скорость Q спустя 5с на автопилоте: " + testCar.speed + " км/ч");
        for (int second = 0; second < 5; second++) {
            testCar.accelerateByAutopilot();
        }
        System.out.println("Скорость Q спустя ещё 5с на автопилоте: " + testCar.speed + " км/ч");

        System.out.println("Переходим в ручной режим:");
        for (int second = 0; second < 2; second++) {
            testCar.accelerate();
        }
        System.out.println("Скорость Q спустя 2с в ручном режиме: " + testCar.speed + " км/ч");
        System.out.println("Проверяем торможение:");
        int brakingTime = 0;
        while (testCar.speed > 0) {
            testCar.brake();
            brakingTime++;
        }
        System.out.println("Время торможения до полной остановки: " + brakingTime + "c");
    }
}
```

#### Класс Transport
```Java
class Transport {
    private double speed;
    private double maxSpeed;
    private double acceleration;
    private double brakingSpeed;
    private int wheelsNumber;

    public void accelerate() {
        if (speed < maxSpeed) {
            speed += acceleration;
        }
    }

    public void brake() {
        if (speed > 0) {
            speed -= brakingSpeed;
        }
    }
}
```

#### Класс Automobile
```Java
class Automobile {
    public Automobile() {
        wheelsNumber = 4;
    }

    protected String direction;

    public void turnTo(String worldSide) {
        direction = worldSide;
    }
}
```
#### Класс Train
```Java
class Train {
    public Train() {
        wheelsNumber = 8;
    }

    private boolean isLocomotive;

    public void turnToLocomotive() {
        isLocomotive = true;
    }

    public void turnToСarriage() {
        isLocomotive = false;
    }
}
```
#### Класс TexlaCar
```Java
class TexlaCar {
    protected double autoPilotMaxSpeed;
    protected double autoPilotAcceleration;

    public TexlaCar() {
        autoPilotMaxSpeed = 60;
        autoPilotAcceleration = 10;
    }

    private void accelerateByAutopilot() {
        if (speed < autoPilotMaxSpeed) {
            speed += autoPilotAcceleration;
        }
    }
}
```
#### Класс TexlaTruck
```Java
class TexlaTruck {
    protected double maxSpeedByDirt;

    public TexlaTruck() {
        maxSpeedByDirt = 30;
    }

    public void accelerateByDirt() {
        if (speed < maxSpeedByDirt) {
            speed += acceleration * 0.5;
        }
    }

    public void brakeByDirt() {
        if (speed > 0) {
            speed -= brakingSpeed * 0.5;
        } 
    }
}
```

#### Класс ModelQ
```Java
class ModelQ {
    public ModelQ() {
        speed = 0;
        maxSpeed = 300;
        acceleration = 100;
        brakingSpeed = 120;
    }
}
```
#### Класс ModelP
```Java
class ModelP {
    public ModelP() {
        speed = 0;
        maxSpeed = 120;
        acceleration = 10;
        brakingSpeed = 50;
    }
}
```


### Подсказки

* Классы Train, TexlaTruck и ModelP никак не участвуют в тестовой программе.
* В классе Transport не может быть полей с модификатором доступа private. Допустимые модификаторы для его полей — public, protected или по умолчанию.
* Чтобы в классе Automobile сработал конструктор, его необходимо наследовать от Transport. Это также даст возможность унаследовать поля speed, maxSpeed, acceleration и brakingSpeed.
* Чтобы использовать метод turnTo(String worldSide), класс TexlaCar должен наследоваться от Automobile.
* Чтобы у экземпляра класса ModelQ появился метод accelerateByAutopilot(), ModelQ должен наследоваться от TexlaCar, а модификатор accelerateByAutopilot() не должен быть private.


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