# Задания по теме "Класс Object и его методы"

# Требования к сдаче работы
Задание выволняется в среде программирования Idea. Результат надо разместить в своем репозитории на GitHub.
Прислать в гугл-формы(размещенная на моем сайте) ссылку на репозиторий.


***Критерии оценивания***
* Оценка 5 - надо сделать все четыре задания.
* Оценка 4 - надо сделать любые три задания.
* Оценка 3 - надо сделать одно любое задание.



# Задание 1
Допишите код класса — бюро находок ```LostAndFoundOffice```. 
В нём должен быть список ```things```
для учёта потерянных вещей, метод ```put()```
для добавления вещи в список, метод ```check()```
— для проверки её наличия. В зависимости от результата ```check()```
должен возвращать ```true``` или ```false```. Методы ```put()```
и ```check()``` должны быть универсальными — принимать в качестве 
параметра объекты любых классов.
Не забудьте предусмотреть ситуацию, если в ```check()```
передана пустая ссылка.

## Заготовка программы

#### Класс **Practicum**
```Java
class Ball { }      // Класс "мяч"
class Accordion { } // Класс "аккордеон"
class Hat { }       // Класс "шляпа"
class Umbrella { }  // Класс "зонт"

public class Practicum {
    // Бюро находок
    static LostAndFoundOffice lostAndFound = new LostAndFoundOffice();

    public static void main(String[] args) {
        Ball ball = new Ball();
        Accordion accordion = new Accordion();
        Umbrella umbrella = new Umbrella();
        Hat hat = new Hat();

        // Сдаём в бюро находок найденные вещи
        lostAndFound.put(ball);
        lostAndFound.put(accordion);
        lostAndFound.put(umbrella);

        checkObject(accordion, "Aккордеон");
        checkObject(ball, "Мяч");
        checkObject(null, "Пустая ссылка");
        checkObject(umbrella, "Зонт");
        checkObject(hat, "Шляпа");
    }

    private static void checkObject(Object object, String description) {
        if(lostAndFound.check(object)) {
            System.out.println('\'' + description + "' нашёлся!");
        } else {
            System.out.println('\'' + description + "' в бюро находок никто не приносил :(");
        }
    }
}
```
#### Класс LostAndFoundOffice
```Java
import java.util.ArrayList;

public class LostAndFoundOffice {
    // создайте список things

    // реализуйте метод put()

    // реализуйте метод check()

    for (Object object : things) { // логика проверки вещи в списке
        if(object.equals(target)) {
            return true;
        }
   
}
```
### Подсказки

* Список потерянных вещей должен хранить любые объекты — ```ArrayList<Object>``` things.
* Чтобы методы ```put()``` и ```check()``` принимали объект любого класса — их параметры должны быть типа ```Object```. К примеру, ```put(Object element)``` и ```check(Object target)```.
* В методе ```check(Object)``` не забудьте проверить, что переданный объект не является пустой ссылкой ```if(target == null)```. Если передана пустая ссылка, должно вернуться ```false```.
* В методе ```check(Object)``` используйте метод ```equals(Object)``` чтобы сравнить объект, переданный в качестве параметра, с элементами списка ```things```.




# Задание 2
Пользователи загрузили в музыкальное приложение большое количество одинаковых треков под разными названиями. Переопределите метод ```equals(Object)``` у класса ```Song```,
чтобы можно было находить одинаковые песни. Вам в помощь в классе ```Practicum``` мы реализовали проверку контракта метода — можете опираться на неё.

#### Класс Practicum
```Java
public class Practicum {
    public static void main(String[] args) {
        Song theRockBandSong = new Song("Popular Song", "The Rock Band", "John Doe");
        Song johnDoeSong = new Song("Popular Song", "The Rock Band", "John Doe");

        Song rapSong = new Song("A song about a hard life", "Popular Rapper", "Popular Rapper");

        Song richardRoeSong = new Song("A song about a hard life", "Popular Rapper", "Richard Roe");

        // проверяем рефлексивность
        boolean check0 = false;
        if (johnDoeSong.equals(johnDoeSong)) {
            check0 = true;
        }

        // проверяем симметричность
        boolean check1 = false;
        if (theRockBandSong.equals(johnDoeSong) &&
                johnDoeSong.equals((Object) theRockBandSong)) {
            check1 = true;
        }

        // проверяем на неравенство объекту другого класса
        boolean check2 = false;
        if (!rapSong.equals(42)) {
            check2 = true;
        }

        // проверяем на неравенство пустой ссылке
        boolean check3 = false;
        if (!theRockBandSong.equals(null)) {
            check3 = true;
        }

        // проверяем на правильное сравнение объектов одного класса
        boolean check4 = true;
        if (richardRoeSong.equals(johnDoeSong)) {
            check4 = false;
        }

        // проверяем транзитивность
        boolean check5 = false;
        Song popularSong = new Song("Popular Song", "The Rock Band", "John Doe");
        if (popularSong.equals(theRockBandSong) && theRockBandSong.equals(johnDoeSong)
                && popularSong.equals(johnDoeSong)) {
            check5 = true;
        }

        // проверяем согласованность
        boolean check6 = true;
        boolean result = rapSong.equals(richardRoeSong);
        for (int i = 0; i < 10; i++) {
            if (rapSong.equals(richardRoeSong) != result) {
                check6 = false;
            }
        }

        if (check0 && check1 && check2 &&
                check3 && check4 && check5 && check6) {
            System.out.println("Поздравляем! Метод equals реализован верно.");
        } else {
            System.out.println("Что-то здесь не так. Подумайте над реализацией ещё немного.");
        }
    }
}
```

#### Класс Song
```Java
import java.util.Objects;

public class Song {
    public final String title;
    public final String artist;
    public final String songwriter;

    public Song(String title, String artist, String songwriter) {
        this.title = title;
        this.artist = artist;
        this.songwriter = songwriter;
    }

    // переопределите метод equals(Object)
    ...
    
}
```


### Подсказки

* Сначала нужно проверить ссылки объектов.
* Если один из объектов — ```null``` или принадлежит к другому классу, — проводить сравнение дальше нет смысла.
* Чтобы получить доступ к полям другого объекта, его нужно привести к типу класса ```(Song)```, экземпляр при этом удобно назвать так же — ```song```.
* С помощью метода ```equals(Object, Object)``` класса ```Objects``` нужно поочерёдно сравнить поля обоих объектов — ```title```, ```song.title```, ```artist```, ```song.artist```,
```songwriter```, ```song.songwriter```.

# Задание 3
Перед вами часть кода программы, которая по имени актера находит фильмы, где он сыграл. Вот только сейчас она не запускается. Исправьте это. 
1. Доработайте класс ```Movie```. Реализуйте конструктор с параметрами, где задаётся название и год выхода фильма. Переопределите методы ```equals(Object)``` и ```hashCode()```.
2. Доработайте класс ```Actor```. Реализуйте конструктор с параметрами, где задаётся имя и фамилия актёра. Переопределите методы ```equals(Object)``` и ```hashCode()```.

#### Класс Practicum
```Java
import java.util.ArrayList;
import java.util.HashMap;

public class Practicum {
    public static void main(String[] args) {
        // Таблицы для хранения рейтингов фильмов и фильмографии актёров
        HashMap<Actor, ArrayList<Movie>> filmography = new HashMap<>();
        HashMap<Movie, Double> ratings = new HashMap<>();

        Movie ivanVasilievichMovie = new Movie("Иван Васильевич меняет профессию", 1973);
        Movie gentlemenOfFortuneMovie = new Movie("Джентльмены удачи", 1971);
        Movie operationYMovie = new Movie("Операция «Ы» и другие приключения Шурика", 1965);
        ratings.put(ivanVasilievichMovie, 8.6);
        ratings.put(gentlemenOfFortuneMovie, 8.5);
        ratings.put(operationYMovie, 8.7);

        Actor aDemyanenko = new Actor("Александр", "Демьяненко");

        ArrayList<Movie> actorMovies = new ArrayList<>();
        actorMovies.add(ivanVasilievichMovie);
        actorMovies.add(operationYMovie);

        filmography.put(aDemyanenko, actorMovies);

        if (filmography.containsKey(new Actor("Александр", "Демьяненко"))) {
            ArrayList<Movie> foundMovies = filmography.get(new Actor("Александр", "Демьяненко"));
            System.out.println("В фильмографии актёра А. Демьяненко найдены следующие фильмы: ");
            for (Movie movie : foundMovies) {
                if (ratings.containsKey(new Movie(movie.title, movie.releaseYear))) {
                    double rating = ratings.get(movie);
                    System.out.println("Фильм " + movie.description() + " с рейтингом " + rating);
                } else {
                    System.out.println("Что-то пошло не так... Проверьте реализацию equals и hashCode в классе Movie.");
                }
            }
        } else {
            System.out.println("Что-то пошло не так... Проверьте реализацию equals и hashCode в классе Actor.");
        }
    }
}
```

#### Класс Actor
```Java
public class Actor {
    String firstName;
    String lastName;
}
```

#### Класс Movie
```Java
public class Movie {
    String title; // название фильма
    int releaseYear; // год выхода на экраны

    public String description() { // метод для вывода описания фильма
        return '"' + title + "\" (" + releaseYear + " год)";
    }
}
```

### Подсказки

* Чтобы создать конструкторы с параметрами, используйте ключевое слово ```this```.
* Метод ```equals(Object)``` после переопределения должен проверять, что сравниваемые объекты равны, ни один не равен пустой ссылке, классы и значения полей объектов полностью совпадают.
* Для переопределения ```hashCode()``` воспользуйтесь методом вспомогательного класса ```Objects```.
* Чтобы использовать методы ```Objects.equals(Object, Object)``` и ```Objects.hash(Object...)```, нужно импортировать класс ```Objects```.
* Поля в ```equals(Object)``` и ```hashCode()``` должны совпадать.


# Задание 4

Перед вами часть программы, которая представляет в текстовом виде информацию об опубликованных на сайте материалах и комментариях к ним. 
Переопределите метод ```toString()``` у классов ```Post``` и ```PostComment``` так, чтобы в консоли появилось текстовое представление объекта ```post```.
Формат вывода — тот, который описывается в уроке (в прекоде есть подсказка). 
Обратите внимание, что поля обоих классов закрыты модификатором ```private``` — организуйте к ним доступ с помощью нужных методов.

# Заготовка программы
#### Класс Practicum
```Java
import java.util.ArrayList;

public class Practicum {
    public static void main(String[] args) {
        Post post = new Post();
        post.setTitle("Почему второй язык программирования выучить проще, чем первый?");
        post.setContent("Если вы научились водить автомобиль на механике, " +
                "вы можете сесть плюс-минус за любой автомобиль и поехать. " +
                "Вам необязательно ездить именно за тем рулём, " +
                "за которым вы учились в автошколе. " +
                "Может быть, первое время вам будет непривычно в новой машине," +
                " но вы быстро освоитесь.");
        post.setTags(new String[]{"Образование", "Карьера в IT"});

        PostComment comment1 = new PostComment();
        comment1.setText("Отличная статья!");
        comment1.setWhoLiked(new String[] { "Lera93", "934Vasya1" });

        PostComment comment2 = new PostComment();
        comment2.setText("Тема не раскрыта :(");
        comment2.setWhoLiked(new String[] { "Petya070707", "Masha90" });

        PostComment comment3 = new PostComment();
        comment3.setText("❤❤❤");

        ArrayList<PostComment> comments = new ArrayList<>();
        comments.add(comment1);
        comments.add(comment2);
        comments.add(comment3);
        post.setComments(comments);

        System.out.println(post);
    }
}
```

#### Класс Post
```Java
public class Post {
    private String title; // заголовок
    private String content; // содержание
    private String[] tags; // теги
    private ArrayList<PostComment> comments; //комментарии
 
/* Вывод должен получиться таким: 
Post{title='xxx', content.length='x', tags=[x,x], 
comments=[PostComment{text='x!', whoLiked=[x, x]}, 
PostComment{text='x', whoLiked=[x,x]}, 
PostComment{text='x', whoLiked=null}]} */

}
```

#### Класс PostComment
```Java
public class PostComment {
    private String text; // содержание комментария
    private String[] whoLiked; // кто поддержал
}
```


### Подсказки

* Чтобы задать значения полям, закрытыми модификатором ```private```, нужно написать ```set-``` методы.
* У поля ```content``` нужно вывести не содержание, а длину. Прежде чем это сделать, проверьте, не передана ли в него пустая ссылка.
* Получить содержание массива нужно с помощью метода ```Arrays.toString()```.
* Чтобы работать с классами ```ArrayList``` и ```Arrays``` в классе, их нужно импортировать.

