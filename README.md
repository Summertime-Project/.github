# .github
Info about project



TODO tłum


##Opracować model komunikacji M-F 
Komunikacja M-F opiera się na zapewnieniu jak najwyższej warstwy abstrakcji przy sterowaniu robotem. Tj M nie ma pojęcia o wewnętrznej strukturze robota w sensie 
fizycznym jak i układu i zależności strowników i oprogramowania. Powinien przkazywać i odbierać jak najmniejszą ilość informacji konieczną do prawidłowego przetwarzania danych z robota i w drugą stronę powinie
powinien zapewniać minimalne i niezależnie informacje sterowania umożliwiające sterownikom jednoznaczne ustalenie porządanego stanu maszyny. Komunikaty będą ustalone po całkowitym ustaleniu wymagań sprzętowych i funkcjonalnych 
. 


##wewnętrzna komunikacja w robocie
Modularność(np zmiana dwóch kół napędowych na gąsienice, lub zmiana kinematyki ramienia) robota wymaga obsługi wewnętrznego protokołu komunikacji przez sterowniki wszystkich modułów. Topologia sieci to gwiazda z centralną jednostką podłączoną do zewnętrznego źródła sterowania
