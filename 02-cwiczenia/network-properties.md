## Ustawianie parametrów sieci

### Zadania

0. Z wykorzystaniem dowolnych systemów operacyjnych na których potrafisz uruchomić interpreter ``python`` oraz oprogramowania virtualbox odwzoruj poniższy schemat sieci:

![alt text][network]

[network]: ./network.png "Logo Title Text 2"

1. na 1 z komputerów zainstaluj i uruchom program ``server.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
2. na 2 z komputerów zainstaluj i uruchom program ``client.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
3. Manipulując konfiguracją sieci na poziomie virtualbox, uruchom serwer czatu, oraz udostępnij go na wybranym porcie oraz adresie tak aby istniała możliwość połączenia przez inne osoby w obrębie pracowni
4. Zainstaluj oprogramowanie serwera HTTP ``nginx`` lub innego, skonfiguruj plik index.html wg instrukcji, sprawdź dostępność strony z wykorzystaniem dowolnego klienta protokołu ``HTTP`` z różnych konfiguracji IP
5. Posługując się programami tj: ``netstat`` lub ``lsof`` sprawdź na jakich portach zostały uruchomione serwery czatu czy HTTP

Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 ||  ip addr add 10.0.15.4/24 dev eth0 |
| IP - address  | 10.0.15.4 |ip addr |
| MASKA  | /24 (255.255.255.0) | |
|   |  | |
| PC 2  || ip addr add 10.0.15.6/24 dev eth0 | 
| IP - address  | 10.0.15.6 | ip addr|
| MASKA  | /24 (255.255.255.0 )| |

Weryfikacja połączenia
------------------------
||Maszyna1|Maszyna2|
| ------------- |:-------------:| -----:|
|Polecenie|ping 10.0.15.6|ping 10.0.15.4|
|Efekt|64 bytes from 10.0.15.6|64 bytes from 10.0.15.4|
|Połączenie|Jest|Jest|
|Internet|Nie ma|Nie ma|
-----------------------------

Konfiguracja interfejsów: /etc/network/interfaces


Statyczna konfiguracja parametrów połączenia
Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 192.168.9.10 | |
| MASKA  | 255.255.255.0 | |
|   |  | |
| PC 2  |  | |
| IP - address  | 10.0.15.4 | |
| MASKA  | 255.255.128.0 | |
| PC 2  |  | |
| IP - address  | 172.16.100.100 | |
| MASKA  | 255.255.0.0 | |

Weryfikacja połączenia
------------------------
||Maszyna1|Maszyna2|
| ------------- |:-------------:| -----:|
|Polecenie|ping 10.0.15.6|ping 10.0.15.4|
|Efekt|64 bytes from 10.0.15.6|64 bytes from 10.0.15.4|
|Połączenie|Jest|Jest|
|Internet|Nie ma|Nie ma|
-----------------------------
Nowa statyczna konfiguracja 

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 192.168.9.12 | |
| MASKA  |255.255.255.0  | |
|   |  | |
| PC 2  |  | |
| IP - address  | 10.0.2.15| |
| MASKA  | 255.255.255.0 | |
| IP - address  | 192.168.9.11 | |
| MASKA  | 255.255.255.0 | |

Weryfikacja połączenia
------------------------
||Maszyna1|Maszyna2.1|Maszyna2.2|
| ------------- |:-------------:|:-----:|----:|
|Polecenie|ping 10.0.15.11|ping google.pl|192.168.9.12|
|Efekt|64 bytes from 192.168.9.11|64 bytes from google.pl|64 bytes from 192.168.9.12|
|Połączenie|Jest|Jest|jest|
|Internet|Nie ma|Jest|Nie ma|
-----------------------------

### Utrwalenie konfiguracji

Aby zmienić addres ip używami komendy: ip addr add ip/maska dev interfejs - przydatne jeżeli DHCP został wyłączony

Resetowanie usługi interfejsów: service networking restart

Podgląd portów: netstat -ltpn 


### Warto wiedzieć

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
| Lokalizacja pliku z konfiguracją sieci| /etc/network/interfaces | |
| UP -> Wyłączenie interfejsu sieciowego|ip link set eth1 up | |
| DOWN -> Włączenie interfejsu sieciowego| ip link set eth1 down| |
| Sprawdzenie obecnych parametrów |ip addr show eth0 |Za eth0 można podstawić inny interfejs |
| lista wszystkich interfejsów | ip a | |
| Które interfejsy jakie porty słuchają | netstat | |

