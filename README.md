# .github
Info about project



TODO tłum

## Mainframe - Main MCU communication

Komunikacja M-F opiera się na zapewnieniu jak najwyższej warstwy abstrakcji przy sterowaniu robotem. Tj M nie ma pojęcia o wewnętrznej strukturze robota w sensie 
fizycznym jak i układu i zależności strowników i oprogramowania. Powinien przkazywać i odbierać jak najmniejszą ilość informacji konieczną do prawidłowego przetwarzania danych z robota i w drugą stronę powinie
powinien zapewniać minimalne i niezależnie informacje sterowania umożliwiające sterownikom jednoznaczne ustalenie porządanego stanu maszyny. Komunikaty będą ustalone po całkowitym ustaleniu wymagań sprzętowych i funkcjonalnych 


## Inter MCU communication

As one of project principles is modularity it's crucial to divide internal robot functions into different MCUs. To achive funcionality despite fragmentation there is need to implement some sort of inter MCU communication. 

### Physical Topology

Physical Topology of simple internal network needs to resemble physical divisions and take into consideration boundaries of interchangeable modules. We also can't assume homogeneity of low lewel protocols(eg. SPI) across all peripheral MCUs. Taking this requirements, we decided to use star network topology with one central MCU connects internal and external connections. This solution mitigate headaches of using different low level protocols. 


### Logical Topology

Logical Topology closely follows Physical Topology as it is also star, one master MCU connects master (Mainframe) to internal pheripherals and manages dataflow.
In future versions we will probaly implement some handshake protocol to make configuration easier.
