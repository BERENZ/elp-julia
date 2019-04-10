
# Pakiety {#tworzenie-pakietow}
<!-- https://journals.plos.org/ploscompbiol/article/file?id=10.1371/journal.pcbi.1006561&type=printable -->
<!-- https://github.com/ropensci/dev_guide -->


Informacje w tym rozdziale powinny pozwolić na stworzenie podstawowego pakietu R.
Istnieje jednak wiele dodatkowych aspektów i kwestii w tym temacie, które zostały tutaj wspomniane pobieżnie lub pominięte.
W celu poznania i zrozumienia złożnych aspektów tworzenia pakietów R cennymi źródłami wiedzy może być książki [R packages](https://r-pkgs.org) [@wickham2015r] oraz [rOpenSci Packages: Development, Maintenance, and Peer Review](https://ropensci.github.io/dev_guide/) [@ropensci_2019_2554759].
Dodatkowo, w niektórych przypadkach pomocna może być oficjalna dokumentacja [Writing R Extensions](https://cran.r-project.org/doc/manuals/R-exts.html#Creating-R-packages) [@team1999writing].

## Tworzenie szkieletu pakietu

[@R-usethis]

<!-- package.skeleton()  Never use this! -->
<!-- usethis::create_package("~/Desktop/mypackage") -->
Funkcja `create_packages()` tworzy cztery pliki:

1. `.Rproj`
2. `R/`
3. `DESCRIPTION`
4. `NAMESPACE`

## Rozwijanie pakietu

<!-- twórz/modyfikuj kod -->
<!-- devtools::load_all() -->
<!-- sprawdź czy działa (unittests)-->
<!-- powtórz -->

## Dokumentacja funkcji

<!-- roxygen2 -->

## Zależności

## Dokumentacja pakietu

<!-- vignettes -->
<!-- usethis::use_vignette("name") -->
<!-- rmarkdown -->
<!-- rstudio helper -->
<!-- pkgdown -->
<!-- readme -->
<!-- news -->

## Wbudowane testy {#wbudowane-testy}

<!-- Unit testing -->
<!-- usethis::use_test() -->
<!-- devtools::test() -->
<!-- devtools::test_coverage() -->
<!-- https://katherinemwood.github.io/post/testthat/ -->
<!-- Automated testing with Travis CI + codecov -->

## Licencje

<!-- There are three main open source licenses -->

<!-- CC0 “public domain”, best for data packages  -->
<!-- MIT Free for anyone to do anything with -->
<!-- GPL Changes and bundles must also be GPL -->
<!-- These are gross simplifications! -->

<!-- DESCRIPTION: -->
<!-- License: file LICENSE -->
<!-- LICENSE: -->
<!-- Proprietary: do not distribute outside of -->
<!-- Widgets Incorporated. -->


## Publikowanie pakietów

\BeginKnitrBlock{rmdinfo}<div class="rmdinfo">software documentation</div>\EndKnitrBlock{rmdinfo}

\BeginKnitrBlock{rmdinfo}<div class="rmdinfo">software promotion</div>\EndKnitrBlock{rmdinfo}

\BeginKnitrBlock{rmdinfo}<div class="rmdinfo">Continuous Integration</div>\EndKnitrBlock{rmdinfo}


## Zadania