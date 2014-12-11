java-course
===========

pragmatic java course (prepared for UMK)



TOC
---

| commitId| step    | description                        |
|:--------|:--------|:-----------------------------------|
| 5c3ce54 | Step 10 | encode controller integration test |
| 9561323 | Step 9  | first integration test             |
| 400640b | Step 8  | status 400 instead of 500          |
| 9561323 | Step 7  | text as path variable              |
| f5b1eec | Step 6  | request parameter added            |
| 810869b | Step 5  | components and second controller   |
| 1c819b8 | Step 4  | building a first controller        |
| 3c4b8a9 | Step 3  | Application class change           |
| ae2b044 | Step 2  | project restructure                |
| ecb3780 | Step 1  | build.gradle for spring app        |


Pobranie aplikacji
------------------

Aby pobraÄ‡ aplikacjÄ™, najlepiej wykonaÄ‡ polecenie:

```
git clone https://github.com/mirog/java-course.git
```

PrzeĹ‚Ä…cz brancha na spring-boot:

```
git checkout spring-boot
```

Projekt zostanie dodany do katalogu java-course znajdujÄ…cego siÄ™ w aktualnym katalogu, w ktĂłrym jesteĹ›.

W systemie windows mamy do operowania git-em osobny terminal "git bash".


Uruchomienie Ĺ›rodowiska
-----------------------

- PrĂłbujemy otworzyÄ‡ projekt w IntelliJ (najlepiej wybierajÄ…c plik build.gradle).
- Puszczamy testy (klikamy w menu kontekstowym katalogu java (test/java) w IntelliJ "Run all tests").
- JeĹĽeli zaĹ›wiecÄ… siÄ™ na zielono, to wszystko jest skonfigurowane.


Uruchomienie programu
---------------------

Aby uruchomiÄ‡ aplikacjÄ™ Spring Boot, wykonujemy polecenie (w windows zamiast ./gradlew mamy ./gradlew.bat):

```
./gradlew bootRun
```


Notatka od Ali:
---------------

Proszę o instrukcję do postępowania w związku z apkami do Heroku :).
Pozdrawiam,
Alicja


Deploy on heroku
----------------

- Potrzebujemy konta w serwisie https://heroku.com/
- Instalujemy Toolbelt heroku i dostajemy dostęp do polecenia heroku w naszej konsoli
- wchodzimy w repozytorium, w którym jest aplikacja, którą chcemy wdrożyć
- polecenie: heroku login - loguje nas i pozwala na dostęp do reszty poleceń
- polecenie: heroku create - tworzy nam na podstawie repozytorium aplikację w heroku
- Jeżeli utworzenie przebiegło pomyślnie to zajmujemy się odpaleniem aplikacji

W projekcie umieszczony jest plik Procfile - plik zawierający kod, wskazujący heroku jak odaplić aplikację.

Dodatkowo dla aplikacji budowanych za pomocą gradla potrzebujemy utworzyć nowy task gradlowy stage, którego wymaga heroku i używa go jako domyślnego odpowiedzialnego za zbudowanie aplikacji.
Nasz task stage będzie zawierać‚ wykonanie dwóch innych istniejących już tasków clean i installApp

```
task stage(dependsOn: ['clean', 'installApp'])
```

Wszystkie pliki powinny być już z commit-owane, jesteśmy na branchu master i wydajemy gitowi polecenie:

```
git push heroku master
```

Nasza aplikacja zbuduje się na serwerach heroku. Wtedy skalujemy liczbę serwerów do 1 aby nasza aplikacja została uruchomiona:

```
heroku ps:scale web=1
```

Dodatkowo możemy śledzić logi aplikacji za pomocą polecenia:

```
heroku logs --tail
```

A aby odtworzyć stronę i nie zastanawiać sić jaki url do niej kieruje wpisujemy:

```
heroku open
```

Każde kolejne wdrożenie świeżej wersji będzie polegać na z commitowaniu plików i zrobieniu push-a (git push heroku master) do serwera zdalnego heroku.

