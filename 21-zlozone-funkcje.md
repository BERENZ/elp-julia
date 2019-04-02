
# (PART) Narzędzia {-}

# Złożone funkcje {#zlozone-funkcje}

<!-- intro -->
<!-- solve a single problem -->
<!-- type stability -->

<!-- 07-oo https://blog.rstudio.com/2019/02/06/rstudio-conf-2019-workshops/ -->

<!-- https://arxiv.org/pdf/1409.3531.pdf -->

## API

Interfejs programistyczny aplikacji (ang. *application programming interface*, API) to zbiór sposobów komunikacji pomiędzy różnymi komponentami oprogramowania.
Inaczej mówiąc API określa w jaki sposób następuje interakcja z kodem.
Dobrze zaprojektowane API uławia zarówno rozwijanie oprogramowania, jak i jego używanie.
Podstawowe elementy przemyślanego API w R obejmują nazwy funkcji, ich argumenty, oraz tzw. stabilność typu (ang. *type stability*.

Funkcje wewnątrz pojedynczego pakietu powinny być nazywane konsekwentnie używając tylko jednej konwencji nazywania (sekcja \@ref(nazwy-obiektow)).
Sama nazwa powinna w zwięzły sposób przekazywać jakie jest działanie funkcji. 
Dodatkową możliwością jest używanie w jednym pakiecie funkcji rozpoczynających się od takiego samego prefiksu. 
Przykładowo, większość nazw funkcji w pakiecie **landscapemetrics** rozpoczyna się od liter `lsm_`, np. `lsm_l_ent()` [@R-landscapemetrics].

Podobnie należy stosować tylko jedną konwencję przy nazywaniu argumentów funkcji, a nazwy argumentów powinny być informacyjne, ale jednocześnie zwięzłe.
W przypadku, gdy taki sam rodzaj danych wejściowych jest oczekiwany w różnych funkcjach, koniecznie jest aby zawsze ten argument był tak samo nazwany.
Podobnie należy zadbać o spójną kolejność podobnych argumentów w funkcjach jednego pakietu.

Stabilność typu oznacza, że używając jednej klasy danych wejściowych funkcja zawsze zwróci obiekt jednej klasy. 
<!-- Przykładowo... -->


```r
tekst = c("kołdra", "kordła", "pościel")
grep("^[k].", x = tekst)
#> [1] 1 2
grep("^[k].", x = tekst, value = TRUE)
#> [1] "kołdra" "kordła"
```

Dodatkowym elementem API może być określenie domyślnych parametrów funkcji.


```r
potegowanie = function(x, w = 2){
  x ^ w
}
```


```r
potegowanie(2)
#> [1] 4
```


```r
potegowanie(2, w = 2)
#> [1] 4
```


```r
potegowanie(2, w = 3)
#> [1] 8
```
<!-- elipsis -->
<!-- https://adv-r.hadley.nz/functions.html#fun-dot-dot-dot -->

## Zasięg widoczności

Zasięg widoczności (ang. *scoping*)

<!-- scope - http://jarekj.home.amu.edu.pl/wp-content/uploads/2018/11/005_funkcje.html -->
<!-- lexical scoping https://adv-r.hadley.nz/functions.html#lexical-scoping -->

## Obsługa błędów, ostrzeżeń i wiadomości

W sekcji \@ref(komunikaty) omówiliśmy trzy podstawowe rodzaje komunikatów: błędy, ostrzeżenia i wiadomości.
Teraz zobaczmy jak te zaimplementować we własnych funkcjach i kiedy powinny być one użyte.

Obsługa błędów w funkcjach ma na celu ochronę użytkownika przed nieodpowiednim zachowaniem funkcji.
Komunikat błędu powinien ułatwiać użytkownikowi zrozumienie problemu oraz jego rozwiązanie. 
Zazwyczaj komunikat błędu przyjmuje jedną z trzech form: (1) określenie problemu, np. "Argument `x` musi być zmienną numeryczną, a nie znakową.", (2) lokalizacja błędu, np. "Kolumna `abc` nie istnieje w obiekcie `y`.", (3) porada, np. "Did you mean `Species == "setosa"`?". 
Oczywiście te wymienione formy można łączyć.

Ważne jest też, aby funkcja kończyła swoje działanie jak najszybciej po napotkaniu, np. błędnych wartości wejściowych.
Żadnej użytkownik nie chce czekać na zakończenie wykonywania długiej funkcji zanim dostanie komunikat błędu.
Więcej informacji o strukturze komunikatów błędów można znaleźć na https://style.tidyverse.org/error-messages.html.

Do zatrzymania działania funkcji i wyświetlenia komunikatu błędu służy `stop()`.


```r
stop("To jest komunikat błędu.")
#> Error in eval(expr, envir, enclos): To jest komunikat błędu.
```

Ostrzeżenia mogą być używane w wielu różnorodnych sytuacjach, np. kiedy chcesz poinformować użytkowników o tym, że dana funkcja zostanie wygaszona lub przeniesiona do innego pakietu.
<!-- Ostrzeżenia są też stosowane w przypadkach, gdy  -->
Komunikaty ostrzeżenia tworzyć się używając funkcji `warning()`.


```r
warning("To jest komunikat ostrzeżenia.")
#> Warning: To jest komunikat ostrzeżenia.
```

Wiadomości mają na celu poinformowanie użytkownika na temat działania pakietu lub funkcji.
Są one wykorzystywane podczas wczytywania niektórych pakietów.<!--..-->
Innym przykładem jest informowanie na temat działania funkcji w tle - pobierania danych, zapisywania do pliku, czy przeliczania cząstkowych parametrów.
Do wyświetlenia wiadomości służy funkcja `message()`.


```r
message("To jest komunikat wiadomości.")
#> To jest komunikat wiadomości.
```

<!-- block cat vs message https://adv-r.hadley.nz/conditions.html#signalling-conditions -->


```r
minus_1 = function(x){
  if(is.character(x)){
    stop("Argument `x` musi być zmienną numeryczną, a nie znakową.")
  } else if(is.logical(x)){
    warning("Argument `x` jest zmienną logiczną. Czy nie chcesz użyć zmiennej numerycznej?")
  } else {
    message("Wow. Argument `x` jest oczekiwaną zmienną numeryczną.")
  }
  abs(x - 1)
}
```


```r
minus_1("kot")
#> Error in minus_1("kot"): Argument `x` musi być zmienną numeryczną, a nie znakową.
```


```r
minus_1(c(TRUE, FALSE))
#> Warning in minus_1(c(TRUE, FALSE)): Argument `x` jest zmienną logiczną. Czy
#> nie chcesz użyć zmiennej numerycznej?
#> [1] 0 1
```


```r
minus_1(c(1, 0, 6, -6))
#> Wow. Argument `x` jest oczekiwaną zmienną numeryczną.
#> [1] 0 1 5 7
```

<!-- http://jarekj.home.amu.edu.pl/wp-content/uploads/2018/10/006_wyjatki.html --> 

\BeginKnitrBlock{rmdinfo}<div class="rmdinfo">R pozwala na ignorowanie wystąpienia błędu używając funkcji `try()`, ignorowanie ostrzeżeń z `suppressWarnings()` oraz wiadomości z `suppressMessages()`.</div>\EndKnitrBlock{rmdinfo}

<!-- https://adv-r.hadley.nz/conditions.html#conditions -->


```r
tryCatch(
  error = function(e) {
    wykonaj kod w przypadku wystąpienia błędu
  },
  kod do uruchomienia 
)
```


```r
test = function(x){
  tryCatch(
  error = function(e) {
    NA
  },
  log(x)
  )
}
```


```r
log(10)
#> [1] 2.3
```


```r
test(10)
#> [1] 2.3
```


```r
log("abecadło")
#> Error in log("abecadło"): non-numeric argument to mathematical function
```


```r
test("abecadło")
#> [1] NA
```

\BeginKnitrBlock{rmdinfo}<div class="rmdinfo">Dodatkowo istnieje funkcja `withCallingHandlers()`, która jest używana w przypadku działania na ostrzeżeniach.</div>\EndKnitrBlock{rmdinfo}

## Programowanie obiektowe

Programowanie obiektowe (ang. *object-oriented programming*, OOP) to jeden z najpopulariniejszych paradygmatów programowania (sekcja \@ref(jezyki-programowania)). 
Polega on na definiowaniu obiektów danej klasy posiadających pewną określoną strukturę oraz zachowania.

<!-- The main ideas of object-oriented programmingare also quite simple and intuitive:1. Everything we compute with is anobject, andobjects should be structured to suit the goals of ourcomputations.2. For this, the key programming tool is aclassdefinition saying that objects belonging to this classshare structure defined bypropertiesthey all have,with the properties being themselves objects of somespecified class.3. A class caninheritfrom (contain) a simplersuperclass, such that an object of this class is alsoan object of the superclass.4. In order to compute with objects, we can de-finemethodsthat are only used when objects are ofcertain classes -->

R pozwala również na stosowanie paradygmatu obiektowego.
Co więcej, w tym języku istnieje kilka różnych systemów programowania obiektowego, między innymi S3, S4 czy R6.
Każdy z nich charakteryzuje inny sposób tworzenia obiektów czy ich zachowań.
W tym rozdziale skupimy się na najczęściej używanego systemu S3.

<!-- W S3 zachowanie działania obiektu powiązane jest  \@ref(inne-klasy)-->
<!-- S3 simplest informal flexible -->


```r
x = matrix(c(0, 0, 2, 3), ncol = 2)
x
#>      [,1] [,2]
#> [1,]    0    2
#> [2,]    0    3
```


```r
class(x)
#> [1] "matrix"
```


```r
y = structure(x, class = "prostokat")
```


```r
class(y)
#> [1] "prostokat"
```

<!-- constructor + validator -->


```r
powierzchnia = function(x) {
  UseMethod("powierzchnia")
}
```


```r
powierzchnia.prostokat = function(x){
  a = x[1, 2] - x[1, 1]
  b = x[2, 2] - x[2, 1]
  a * b
}
```


```r
y
#>      [,1] [,2]
#> [1,]    0    2
#> [2,]    0    3
#> attr(,"class")
#> [1] "prostokat"
powierzchnia(y)
#> [1] 6
```


```r
x
#>      [,1] [,2]
#> [1,]    0    2
#> [2,]    0    3
powierzchnia(x)
#> Error in UseMethod("powierzchnia"): no applicable method for 'powierzchnia' applied to an object of class "c('matrix', 'double', 'numeric')"
```

<!-- methods -->
<!-- https://arxiv.org/pdf/1409.3531.pdf -->
<!-- https://adv-r.hadley.nz/oo.html -->

## Testy jednostkowe

<!-- Unit testing -->
<!-- usethis::use_test() -->
<!-- devtools::test() -->
<!-- devtools::test_coverage() -->

## Zadania