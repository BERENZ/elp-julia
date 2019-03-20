
# Powtarzanie {#petle}

<!-- intro -->
<!-- https://recology.info/2019/03/control-flow-exceptions/ -->

## Pętla for

### Składnia

<!-- https://rpubs.com/daspringate/vectorisation -->


```r
for (element in wektor) {
  przetwarzanie elementu
}
```

### Przykład działania

<!-- mila lądowa = 1,609 km -->


```r
odl_mile = c(142, 63, 121)
```


```r
for (i in odl_mile) {
  print(i * 1.609)
}
#> [1] 228
#> [1] 101
#> [1] 195
```

<!-- i block -->


```r
for (i in 1:3) {
  print(odl_mile[i] * 1.609)
}
#> [1] 228
#> [1] 101
#> [1] 195
```

<!-- block -->
<!-- uzywaj seq_along(old_mile) zamiast 1:length(old_mile), bo -->
<!-- 1:lenght(0) -->


```r
odl_mile_l = seq_along(odl_mile)
for (i in odl_mile_l) {
  print(odl_mile[i] * 1.609)
}
#> [1] 228
#> [1] 101
#> [1] 195
```


```r
odl_mile_l = seq_along(odl_mile)
for (i in odl_mile_l) {
  odl_mile[i] = odl_mile[i] * 1.609
}
odl_mile
#> [1] 228 101 195
```


```r
odl_mile = c(142, 63, 121)
```


```r
odl_km = vector("numeric", length = 0)
odl_mile_l = seq_along(odl_mile)
for (i in odl_mile_l) {
  odl_km = c(odl_km, odl_mile[i] * 1.609)
}
odl_km
#> [1] 228 101 195
```


```r
odl_mile = c(142, 63, 121)
```


```r
odl_km = vector("numeric", length = length(odl_mile))
odl_mile_l = seq_along(odl_mile)
for (i in odl_mile_l) {
  odl_km[i] = odl_mile[i] * 1.609
}
odl_km
#> [1] 228 101 195
```

### Zastosowanie w funkcjach


```r
mile_na_km = function(odl_mile){
  odl_km = vector("numeric", length = length(odl_mile))
  odl_mile_l = seq_along(odl_mile)
  for (i in odl_mile_l) {
    odl_km[i] = odl_mile[i] * 1.609
  }
  odl_km
}
```


```r
odleglosci_mile = c(0, 1, 10, 55, 160)
mile_na_km(odleglosci_mile)
#> [1]   0.00   1.61  16.09  88.50 257.44
```



## Pętla while 

<!--     pętla for stosowana w sytuacji, gdy ilość wykonań kodu jest znana przed rozpoczęciem działania pętli -->
<!--     pętle while i repeat są stosowana gdy ilość wykonań nie jest znana przed zakończeniem działania pętli -->
<!-- są one bardziej elastyczne, ale też rzadziej używane -->

<!-- https://rstudio-education.github.io/hopr/loops.html#while-loops -->

<!-- `next`, `break` -
https://adv-r.hadley.nz/control-flow.html#loops -->
<!-- `while`, `repeat` -->

<!-- block - R nie ma do {action} while (condition) -->


```r
while (warunek){
    wykonuj operację tak długo jak warunek jest spełniony
}
```




```r
budzet = 100
liczba_dni = 0
while(budzet > 0 && budzet < 200){
  budzet = budzet + sample(-10:10, size = 1)
  liczba_dni = liczba_dni + 1
}
liczba_dni
#> [1] 535
```

## Programowanie funkcyjne

<!-- \@ref(dzialania-na-wektorach) -->
<!-- wektoryzacja-->
<!-- http://www.noamross.net/blog/2014/4/16/vectorization-in-r--why.html -->
<!-- http://alyssafrazee.com/2014/01/29/vectorization.html -->
<!-- *apply -->


```r
pomiary = data.frame(
  miastoA = c(6.1, 1.4, -2.1),
  miastoB = c(4.3, 5.2, 3.0),
  miastoC = c(4.1, 4.2, 3.3)
  )
```


```r
sr_miasto = vector("numeric", length = ncol(pomiary))
for(i in seq_len(ncol(pomiary))){
  sr_miasto[i] = mean(pomiary[, i])
}
sr_miasto
#> [1] 1.80 4.17 3.87
```


```r
sr_dzien = vector("numeric", length = nrow(pomiary))
for(i in seq_len(nrow(pomiary))){
  sr_dzien[i] = mean(unlist(pomiary[i, ]))
}
sr_dzien
#> [1] 4.83 3.60 1.40
```


```r
apply(pomiary, MARGIN = 2, FUN = mean)
#> miastoA miastoB miastoC 
#>    1.80    4.17    3.87
```


```r
apply(pomiary, MARGIN = 1, FUN = mean)
#> [1] 4.83 3.60 1.40
```

## Zadania

<!-- peer instruction - https://journals.plos.org/ploscompbiol/article/file?id=10.1371/journal.pcbi.1006023&type=printable -->

1) Spójrz na poniższy kod, ale nie wykonuj go.
Ile razy zostanie wyświetlony tekst `"Działa!"`?


```r
for (i in c(1, 2, 4, 5, 6)){
    if (i < 2 | i >= 5)
      print("Działa!")
}
```

2) Spójrz na poniższy kod, ale nie wykonuj go.
Ile razy zostanie wyświetlony tekst `"Działa!"`?


```r
for (i in c(1, 2, 4, 5, 6)){
  for (j in 6:3){
    if (i < 2 | i >= 5)
      print("Działa!")
  }
}
```

3) Spójrz na poniższy kod, ale nie wykonuj go.
Ile razy zostanie wyświetlony tekst `"Działa!"`?


```r
for (i in c(1, 2, 4, 5, 6)){
  for (j in 6:3){
    if (i < 2 & j >= 5)
      print("Działa!")
  }
}
```

4) Spójrz na poniższy kod, ale nie wykonuj go.
Ile razy zostanie wyświetlony tekst `"Działa!"`?


```r
for (i in c(1, 2, 4, 5, 6)){
  for (j in 6:3){
    if (i < 2 | j >= 5)
      print("Działa!")
  }
}
```

5) Spójrz na poniższy kod, ale nie wykonuj go.
Ile razy zostanie wyświetlony tekst `"Działa!"`?


```r
for (i in c(1, 2, 3)){
  for (j in 6:3){
    i = i + j
    if (i < 4 | i >= 9)
      print("Działa!")
  }
}
```