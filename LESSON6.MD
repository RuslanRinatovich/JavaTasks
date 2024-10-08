# Задания по теме "Наследование"

# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все пять задания.
* Оценка 4 - надо сделать любые три задания.
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
В 2013 году норвежский дуэт братьев Илвисокеров Ylvis выпустил на YouTube вирусный клип “What Does the Fox Say?” (англ. «Что говорит лиса?») — к настоящему моменту его посмотрели более 1 млрд раз. Сюжет песни посвящен тому, что отлично известно, как говорят многие животные: собака — «гав», кошка — «мяу», корова — «му», а вот как говорит лиса — великая тайна. Немного передохните — послушайте песенку, а потом с помощью наследования и переопределения методов запрограммируйте её первый куплет:

```
Dog goes woof
Cat goes meow
Bird goes tweet
And mouse goes squeek
Cow goes moo
Frog goes croak
And the elephant goes toot
Ducks say quack
And fish go blub
And the seal goes ow ow ow
```
Не забудьте использовать аннотацию ```@Override```!

#### Класс Practicum
```Java
public class Practicum {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Cat cat = new Cat();
        Bird bird = new Bird();
        Mouse mouse = new Mouse();
        ... // инициализируйте все нужные объекты
        System.out.println("Dog goes " + dog.say());
        System.out.println("Cat goes " + cat.say());
        System.out.println("Bird goes " + bird.say());
        System.out.println("And mouse goes " + mouse.say());
        ... // вызовите переопределённые методы
    }
}
```

#### Класс Animal
```Java
public class Animal {
    public String say() {
        return "I'm an Animal!";
    }
}

// Сделайте так, чтобы классы наследовали от Animal и переопределите в них метод say().
```

#### Класс Dog
```Java
class Dog {

}
```

#### Класс Cat
```Java
class Cat {
    
}
```


### Подсказки

* 10 подклассов должны наследовать от ```Animal``` с помощью ключевого слова ```extends```.
* Имена подклассов должны совпадать с названиями животных в единственном числе: ```Dog```, ```Cat```, 
```Bird```, ```Mouse```, ```Cow```,```Frog```, ```Elephant```, ```Duck```, ```Fish```, ```Seal```.
* Необходимо переопределить метод ```say()``` в каждом подклассе.
* Перед переопределяемым методом нужно поставить аннотацию ```@Override```.
* При переопределении не нужно менять модификатор доступа и сигнатуру метода.


# Задание 4

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



# Задание 5
Перед вами прекод робокиоска “SOUPER-3000”, который специализируется на приготовлении разных супов и бульонов. Вам нужно дополнить его конструкторами. В родительском классе SoupBase реализуйте один конструктор — для создания основы под любой суп. В подклассах создайте по несколько конструкторов.  Один должен принимать все ингредиенты по отдельности, а другие добавлять новые ингредиенты к уже готовому супу или основе. В результате должно быть напечатано восемь разных рецептов — данные для них уже занесены в программу.


#### Класс Practicum
```Java
public class Practicum {
    public static void main(String[] args) {
        System.out.println("Готовим основу:");
        SoupBase soupBase = new SoupBase(2, 5);
        soupBase.printIngredients();

        System.out.println("\nИз основы приготовим вегетарианский суп и бульон:");
        Bouillon bouillon = new Bouillon(soupBase, 300);
        bouillon.printIngredients();
        VegetarianSoup vegetarianSoup = new VegetarianSoup(soupBase, 200);
        vegetarianSoup.printIngredients();

        System.out.println("\nПриготовим вегетарианский суп с нуля");
        VegetarianSoup vegetarianSoupWithoutBase = new VegetarianSoup(1.5, 5, 200);
        vegetarianSoupWithoutBase.printIngredients();

        System.out.println("\nПриготовим другой бульон для картофельного супа:");
        Bouillon anotherBouillon = new Bouillon(5, 10, 800);
        anotherBouillon.printIngredients();

        System.out.println("\nИз этого бульона приготовим суп с картошкой:");
        PotatoSoup potatoSoup = new PotatoSoup(anotherBouillon, 4, 1);
        potatoSoup.printIngredients();

        System.out.println("\nСуп с картошкой можно приготовить и из суповой основы:");
        PotatoSoup potatoSoupFromBase = new PotatoSoup(soupBase, 200, 3, 0);
        potatoSoupFromBase.printIngredients();

        System.out.println("\nА можно и совсем с нуля:");
        PotatoSoup totallyNewPotatoSoup = new PotatoSoup(5, 10, 400, 5, 1);
        totallyNewPotatoSoup.printIngredients();
    }
}
```

#### Класс SoupBase
```Java
public class SoupBase {
    double water;
    double salt;

    // реализуйте конструктор

    public void printIngredients() {
        System.out.println("Ингредиенты суповой основы:");
        System.out.println("Вода: " + water + " л.");
        System.out.println("Соль: " + salt + " г.");
    }
}
```

#### Класс Bouillon
```Java
public class Bouillon extends SoupBase {
    double meat;

    // реализуйте необходимые конструкторы

    @Override
    public void printIngredients() {
        System.out.println("Ингредиенты бульона:");
        System.out.println("Вода: " + water + " л.");
        System.out.println("Соль: " + salt + " г.");
        System.out.println("Мясо: " + meat + " г.");
    }
}
```

#### Класс VegetarianSoup
```Java
public class VegetarianSoup extends SoupBase {
    double vegetables;

    // реализуйте необходимые конструкторы

    @Override
    public void printIngredients() {
        System.out.println("Ингредиенты вегетарианского супа:");
        System.out.println("Вода: " + water + " л.");
        System.out.println("Соль: " + salt + " г.");
        System.out.println("Овощи: " + vegetables + " г.");
    }
}
```

#### Класс PotatoSoup
```Java
public class PotatoSoup extends Bouillon {
    double potato;
    double carrot;

    // реализуйте необходимые конструкторы

    @Override
    public void printIngredients() {
        System.out.println("Ингредиенты картофельного супа:");
        System.out.println("Вода: " + water + " л.");
        System.out.println("Соль: " + salt + " г.");
        System.out.println("Мясо: " + meat + " г.");
        System.out.println("Картошка: " + potato + " шт.");
        System.out.println("Морковка: " + carrot + " шт.");
    }
}
```


### Подсказки

* Формат сигнатуры конструкторов можно найти в инициализации объектов каждого класса.
* Конструктор ```SoupBase``` должен принимать два параметра: ```double water``` и ```double salt```.
* Для создания конструкторов в подклассах нужно использовать ключевое слово ```super```.
* Если в конструктор передаётся объект — например, ```Bouillon bouillon```, 
то нужно обратиться к его полям через имя и точечную нотацию — ```bouillon.water```, 
```bouillon.salt```, ```bouillon.meat```.
* В классе ```PotatoSoup``` должно быть три конструктора.
