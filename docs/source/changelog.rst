Changelog
=========

Version 1.2.13
-------------

:Date: Jan 10, 2023

* [RIS-2497](https://radpoint.atlassian.net/browse/RIS-2497) [REG] Automatyczne wypełnianie dawek w formularzu zlecenia w oparciu o dane DICOM

	W formularzu zlecenia w module rejestracji dodano funkcjonalność automatycznego wypełniania sekcji dotyczącej dawki dla badąń TK i RTG. Obecnie system umożliwa wklejanie wstępnych wyniki analizy autorskiego algorytmu AI DOSE DR / AI DOSE CT w sekcji dotyczącej ewidencji dawek. Dostęp do funkcjonalności wymaga odpowiedniej licencji.    
  
* [RIS-2572](https://radpoint.atlassian.net/browse/RIS-2572) Rozszerzenie modelu bazy danych (jednostki kierujące) 

* [RIS-2587](https://radpoint.atlassian.net/browse/RIS-2587) [REG] Zmiany widoku dokumentów załaczonych do badania 

* [RIS-2563](https://radpoint.atlassian.net/browse/RIS-2563) [RPT] Nowy filtr dla zleceń teleradiologicznych "Rodzaje zlecen" 

	**Opisy lokalne \(Lokalne\)** - zlecenia wysyłane do RPT bez kontekstu umowy teleradiologicznej , zdecydowana większość zleceń opisu generowana w zwykłej pracowni lokalnie u klienta RIS/PACS, który nie zleca do opisu w teleradiologii i nie świadczy usług teleradiologii na rzecz innych podmiotów \(np. jako lekarz pracujący w Ostrołęce w lokalnej pracowni TK widzę badania przesłane do opisu z tej pracowni TK - technik wysłał do opisu lokalnego\)

	**Zlecenia teleradiologiczne \(Teleradiologia\)** -  czyli zlecenia świadczone pomiędzy różnymi podmiotami, przesyłane do RPT przez zewnętrzne podmioty zlecające \(innych klientów\). Czyli jesli np. z sochaczewa wyśle technik badanie do opisu do voxela, to będzie to zlecenie widoczne w RPT voxela jako zlecenie teleradiologiczne.

	| **Label przycisku “Rodzaj zleceń”** | `serviceType` | `provider` | `recipient` |
	| --- | --- | --- | --- |
	| Lokalne | null | null | null |
	| Lokalne i teleradiologia | `TELERADIOLOGY` lub null | `provider.id` = klient id LUB null | `recipient.id` **!=** klient id LUB null |
	| Teleradiologia | `TELERADIOLOGY` | `provider.id` = klient id  | `recipient.id` **!=** klient id |
	| XXX - gdzie XXX odpowiada `serviceName` umowy z API | `TELERADIOLOGY` | `provider.id` = klient id | `recipient.id` = klient id  |

Domyślnie dla każdego klienta ten filtr nie powinien być wybrany. Pozycje na filtrze powinny się pojawiać, tylko jeśli stosowne zlecenia istnieją. 

Dodatkowo w ustawieniach Modułu opisów nowa sekcja pozwalająca na domyślne ustawienie filtracji zleceń:

* [RIS-2596](https://radpoint.atlassian.net/browse/RIS-2596) [REG] W oknie ewidencji dawek dodano przycisk "Wypełnij automatycznie" który pozwala na dodanie informacji dt. dawek i ekspozycji badania w oparciu o dane z DICOM, niezależnie od wcześniej wklejonych wartosci 

* [RIS-2597](https://radpoint.atlassian.net/browse/RIS-2597) [REG] Mechanizm zaokrąglania wartości CTDI jak i SSDE do wartości dziesietnych 