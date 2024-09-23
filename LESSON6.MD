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

* Классы ```Train```, ```TexlaTruck``` и ```ModelP``` никак не участвуют в тестовой программе.
* В классе ```Transport``` не может быть полей с модификатором доступа ```private```. Допустимые модификаторы для его полей — ```public```, ```protected``` или по умолчанию.
* Чтобы в классе ```Automobile``` сработал конструктор, его необходимо наследовать от ```Transport```. Это также даст возможность унаследовать поля ```speed```, ```maxSpeed```, ```acceleration``` и ```brakingSpeed```.
* Чтобы использовать метод ```turnTo(String worldSide)```, класс ```TexlaCar``` должен наследоваться от ```Automobile```.
* Чтобы у экземпляра класса ```ModelQ``` появился метод ```accelerateByAutopilot()```, ```ModelQ``` должен наследоваться от ```TexlaCar```, а модификатор ```accelerateByAutopilot()``` не должен быть ```private```.


# Задание 3

Систему тестирования модели “Q” от “Texla” доработали и убрали лишнее.
Код теперь запускается, но есть проблема — результаты тестов не совпадают 
с ожидаемыми. Из-за технического сбоя файл ```Automobile``` оказался недоступен. 
Вносить изменения в класс Practicum также нельзя. 
Менять код можно только в файлах ```Texla``` и ```ModelQ```.
Исправьте код таким образом, чтобы все тесты 
проходили успешно. Учитывайте, что сейчас метод 
```accelerateByAutopilot()``` не учитывает максимальную скорость автопилота.
Добавьте в него условие, чтобы ускорение происходило, 
только если скорость автомобиля меньше максимальной скорости
автопилота. Если условие не выполняется, то значит, 
что скорость равна максимальной. Затем переопределите методы
```accelerate()``` и  ```brake()```.
Итоговый вывод в консоли должен быть таким:
 ```
Характеристики модели:
Ускорение: 100.0 км/(ч*с)
Максимальная скорость: 300.0 км/ч

Начало теста!
Едем на автопилоте:
Скорость Q спустя 5с на автопилоте: 55.0 км/ч ✅
Скорость Q спустя ещё 5с на автопилоте: 60.0 км/ч ✅
Переходим в ручной режим:
Скорость Q спустя 2с в ручном режиме: 260.0 км/ч ✅
Скорость Q спустя ещё 2с в ручном режиме: 300.0 км/ч ✅
Проверяем торможение:
Время торможения до полной остановки: 3c ✅
Скорость Q: 0.0 км/ч ✅ 
 ```

# Заготовка программы
#### Класс Practicum
```Java
class Practicum {
    public static void main(String[] args) {
        ModelQ testCar = new ModelQ();

        System.out.println("Характеристики модели:");
        System.out.println("Ускорение: " + testCar.acceleration + " км/(ч*с)");
        System.out.println("Максимальная скорость: " + testCar.maxSpeed + " км/ч");

        System.out.println("\nНачало теста!");

        System.out.println("Едем на автопилоте:");
        for (int second = 0; second < 5; second++) {
            testCar.accelerateByAutopilot();
        }
        System.out.print("Скорость Q спустя 5с на автопилоте: " + testCar.speed + " км/ч");
        checkResult(55.0, testCar.speed);

        for (int second = 0; second < 5; second++) {
            testCar.accelerateByAutopilot();
        }
        System.out.print("Скорость Q спустя ещё 5с на автопилоте: " + testCar.speed + " км/ч");
        checkResult(60.0, testCar.speed);


        System.out.println("Переходим в ручной режим:");
        for (int second = 0; second < 2; second++) {
            testCar.accelerate();
        }
        System.out.print("Скорость Q спустя 2с в ручном режиме: " + testCar.speed + " км/ч");
        checkResult(260.0, testCar.speed);

        for (int second = 0; second < 2; second++) {
            testCar.accelerate();
        }
        System.out.print("Скорость Q спустя ещё 2с в ручном режиме: " + testCar.speed + " км/ч");
        checkResult(300.0, testCar.speed);


        System.out.println("Проверяем торможение:");
        int brakingTime = 0;
        while (testCar.speed > 0) {
            testCar.brake();
            brakingTime++;
        }
        System.out.print("Время торможения до полной остановки: " + brakingTime + "c");
        checkResult(3, brakingTime);
        System.out.print("Скорость Q: " + testCar.speed + " км/ч");
        checkResult(0.0, testCar.speed);
    }

    private static void checkResult(double expect, double actual) {
        if (expect == actual) {
            System.out.println(" ✅");
        } else {
            System.out.println(" ❌");
        }
    }

    private static void checkResult(int expect, int actual) {
        if (expect == actual) {
            System.out.println(" ✅");
        } else {
            System.out.println(" ❌");
        }
    }
}
```

#### Класс Automobile
```Java
// данный класс недоступен для изменений
class Automobile {
    protected double speed;
    protected double maxSpeed;
    protected double acceleration;
    protected double brakingSpeed;


    public Automobile() {
        acceleration = 30;
        brakingSpeed = 120;
    }

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

#### Класс Texla
```Java
class Texla extends Automobile {
    protected double autoPilotMaxSpeed;
    protected double autoPilotAcceleration;

    public Texla() {
        autoPilotMaxSpeed = 60;
        autoPilotAcceleration = 11;
    }

    public void accelerateByAutopilot() {
        speed += autoPilotAcceleration;
        // исправьте метод для ускорения при автопилоте
    }

    // переопределите метод для ускорения

    // переопределите метод для торможения
}
```

#### Класс ModelQ
```Java
class ModelQ extends Texla {

    public ModelQ() {
        // переопределите необходимые поля
        speed = 0;
    }
}
```

### Подсказки

* Максимальная скорость в ручном режиме — 300 км/ч, значит,
необходимо в конструкторе ```ModelQ``` установить в ```maxSpeed``` значение 300.
* После поездки на автопилоте скорость
автомобиля должна быть 60 км/ч, а после 2 секунд в ручном
режиме должна стать 260 км/ч. 
Значит, в конструкторе ```ModelQ``` нужно установить в ```acceleration``` значение 100.
* Ускорение на автопилоте происходит, 
только если скорость автомобиля меньше максимальной 
скорости ```if (speed < autoPilotMaxSpeed) {speed += autoPilotAcceleration;}```
, в обратном случае ```else {speed = autoPilotMaxSpeed;}```.
* При ускорении: если скорость меньше максимальной ```if (speed < maxSpeed)```,
машина разгоняется ```speed += acceleration```, пока не достигнет 
максимума ```speed = maxSpeed```.
* При торможении: если скорость больше нуля ```if (speed > 0)```, 
машина сбрасывает скорость 
```speed -= brakingSpeed``` до полной остановки ```speed = 0```.
* Не забудьте добавить аннотацию ```@Override``` перед переопределяемыми методами.