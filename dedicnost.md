# Dědičnost

## Cenný balík

Pokračuj ve své práci pro zásilkovou společnost. Společnost nově doručuje i cenné balíky, které mají zadanou určitou hodnotu.

- Vytvoř třídu `ValuablePackage`, která dědí od třídy `Package`. `ValuablePackage` má navíc atribut `value`, ostatní atributy dědí od třídy `Package`.
- Atribut `value` nastav pomocí funkce `__init__`. Ostatní parametry předej funkci `__init__` třídy `Package`.
- Přidej do výpisu informací o cenném balíku (metoda `__str__`) informaci o ceně balíku.
- Vytvoř si alespoň jeden objekt a zkus volání jeho funkcí. Současně si vytvoř "obyčejný" balík o zkontroluj, že u něj se nic nezměnilo.

```py
class Package:
    def __init__(self, address, weight, state):
        self.address = address
        self.weight = weight
        self.state = state

    def get_info(self):
        return f"Balík na adresu {self.address} má hmotnost {self.weight} kg a je ve stavu {self.state}."

class ValuablePackage(Package):
    def __init__(self, address, weight, value, state="nedoručen"):
        super().__init__(address, weight, state)
        self.value = value

    def __str__(self):
        return super().__str__() +  f"Balík má hodnotu hodnotu {self.value} Kč."

# Vytvoření objektů
valuable_package = ValuablePackage("Václavské Náměstí 12, Praha", 0.25, 5000)
package = Package("Jiřího z Poděbrad 9, Brno", 1.5, "doručen")

# Výpis informací o balících
print(valuable_package)
print(package)

print(valuable_package.deliver())
print(valuable_package)  # Zkontrolujeme, že balík je nyní ve stavu "doručen"
print(valuable_package.deliver())  # Zkusíme znovu doručit balík
```

## Jízdenky a letenky

Nyní je naším cílem práce pro společnost, která se zabývá prodejem jízdenek a letenek.

- Vytvoř třídu `Ticket`, která bude mít atributy `basic_price` (základní cena) a `seat_number` (číslo sededla). Tato třída bude sloužit například pro cesty autobusem.
- Při cestování vlakem musíme řešit, jestli cestující využívá 1. nebo 2. třídu. Vytvoř třídu `TrainTicket`, která bude mít navíc atribut `fare_class` (uvažujeme možnosti `economy` a `business`). Dále naprogramuj metodu `get_price()`, která bude vracet hodnotu stejnou jako `basic_price`, pokud atribut `fare_class` je `economy`, a cenu o 20 % vyšší oproti `basic_price`, pokud `fare_class` je `business`.
- U letenek řešíme třídu, kterou cestující letí, navíc ale musíme řešit i počet odbavených zavazadel. Vytvoř třídu `PlaneTicket`, která bude dědit od třídy `TrainTicket` a bude mít navíc atribut `checkout_luggages`, který udává počet odbavených zavazadel. Naprogramuj metodu `get_price()`, která bude vracet hodnotu stejnou jako `basic_price`, pokud atribut `fare_class` je `economy`, a cenu o 50 % vyšší oproti `basic_price`, pokud `fare_class` je `business`. Dále připočti 2000 za každé odbavené zavazadlo (bez ohledu na třídu).
- Vytvoř jízdenku na vlak se základní cenou 150 do tříd `economy` i `business`. Zkontroluj, jakou hodnotu vrací metoda `get_price()`.
- Vytvoř letenku se základní cenou 6000 do tříd `economy` i `business` s jedním odbaveným zavazadlem. Zkontroluj, jakou hodnotu vrací metoda `get_price()`.


```py
class Ticket:
    def __init__(self, basic_price, seat_number):
        self.basic_price = basic_price
        self.seat_number = seat_number


class TrainTicket(Ticket):
    def __init__(self, basic_price, seat_number, fare_class):
        super().__init__(basic_price, seat_number)
        self.fare_class = fare_class

    def get_price(self):
        if self.fare_class == 'economy':
            return self.basic_price
        elif self.fare_class == 'business':
            return self.basic_price * 1.2


class PlaneTicket(TrainTicket):
    def __init__(self, basic_price, seat_number, fare_class, checkout_luggages):
        super().__init__(basic_price, seat_number, fare_class)
        self.checkout_luggages = checkout_luggages

    def get_price(self):
        luggage_price = self.checkout_luggages * 2000
        if self.fare_class == 'economy':
            return self.basic_price + luggage_price
        elif self.fare_class == 'business':
            return self.basic_price * 1.5 + luggage_price


# Testování:
train_ticket_economy = TrainTicket(150, '1A', 'economy')
train_ticket_business = TrainTicket(150, '1A', 'business')
print(train_ticket_economy.get_price())  # 150
print(train_ticket_business.get_price())  # 180

plane_ticket_economy = PlaneTicket(6000, '15B', 'economy', 1)
plane_ticket_business = PlaneTicket(6000, '15B', 'business', 1)
print(plane_ticket_economy.get_price())  # 8000
print(plane_ticket_business.get_price())  # 11000
```

## Cena přepravy

Pokračuj ve své práci pro zásilkovou společnost. Společnost nově požaduje, aby náš software uměl dopočítat cenu přepravy balíku.

- Do třídy `Package` přidej metodu `get_costs()`. Vypočítej přepravu na základě hmotnosti. Přeprava balíku do 2 kg stojí 150 Kč, balíků mezi 2 a 5 kg 190 Kč a těžších balíků 220 Kč. Zkontroluj, zda metoda funguje i pro cenné balíky.
- U cenných balíků bude k ceně připočtení pojištění. Přidej ke třídě `ValuablePackage` metodu `get_costs()`. Ta spočítá cenu přepravy s využitím metody mateřské třídy `Package`. K tomu připočte pojistné ve výši 5 % ceny balíku.

```py
class Package:
    def __init__(self, address, weight, state):
        self.address = address
        self.weight = weight
        self.state = state

    def __str__(self):
        return f"Balík na adresu {self.address} má hmotnost {self.weight} kg a je ve stavu {self.state}."

    def get_costs(self):
        cost = 0
        if self.weight <= 2:
            cost = 150
        elif self.weight <= 5:
            cost = 190
        else:
            cost = 220
        return cost
    
    def deliver(self):
        if self.state == "doručen":
            return "Balík již byl doručen"
        
        self.state = "doručen"
        return "Doručení uloženo"

class ValuablePackage(Package):
    def __init__(self, address, weight, state, value):
        super().__init__(address, weight, state)
        self.value = value
    
    def __str__(self):
        return super().__str__() + f" Balíček má hodnotu {self.value} Kč."
    
    def get_costs(self):
        price = super().get_costs()
        return price * 1.05
```

## Audioknihy

V některých případech je nutné sáhnout k úpravám již napsané třídy. Uvažujme nakladatelství, pro které jsme vytvořili třídu `Book` v minulé lekci. Třída měla atributy `title`, `pages` and `price`. Nyní uvažujeme, že se nakladatelství rozhodlo vydávat i audioknihy. Ty nemají počet stránek, ale musíme u nich evidovat herce nebo herečku, který/která audioknihu předčítá. Budeme tedy chtít vytvořit třídu `AudioBook`, ale ta by neměla přímo dědit od třídy `Book`, protože by nám tam zbyl nepotřebný atribut `pages`. Musíme tedy prové úpravu již existujícího kódu. Takové úpravě se někdy říká *refaktorizace*.

Vytvoř třídu `Item`, což je obecná položka, kterou bude nakladatelství prodávat. Třída `Item` bude mít atributy `title` a `price`. Uprav třídu `Book` tak, aby dědila od třídy `Item`. Třída `Book` bude mít navíc atribut `pages`. Atributy `title` a `price` nastav s využitím metody `__init__` rodičovské třídy `Item`. Dále přidej třídu `AudioBook`, která bude mít navíc atributy `duration_in_hours` (délka nahrávky v hodinách) a `narrator` (člověk, který knihu čte). Třída `AudioBook` bude opět dědit od třídy `Item` a atributy `title` a `price` bude nastavovat s využitím metody `__init__` rodičovské třídy `Item`.

Třída `Book` si zachová svoji metodu `get_time_to_read()`, která pracuje s počtem stran (`pages`). Třída `AudioBook` bude mít metodu `get_time_to_read()` taky a při jejím zavolání bude vracet hodnotu atributu `duration_in_hours`. Pokud mají metodu všichni potomci, je běžné metodu přidat i rodičovské třídě. Přidej tedy metodu `get_time_to_read()` třídě `Item`. Do metody vlož klíčové slovo `pass`, protože pro třídu `Item` nebudeme do metody vkládat žádný výpočet.

Vytvoř objekty reprezentující audioknihu Problém tří těles (délka 14.4, čte Zbyšek Horák, cena 299 Kč) a knihu Kadet Hornblower (242 stran, cena 399 Kč). Uvažuj, že nakladatelství přidá do e-shopu funkci, která vrátí celkový čas, kdy si bude moci zákazník nebo zákaznice užívat nakoupené produkty. Vytvoř tedy proměnnou `total_time`, která bude obsahovat součet délky audioknihy a času potřebného na přečtení knihy. Obojí zjisti s využitím metody `get_time_to_read()`.

```py
class Item:
    def __init__(self, title, price):
        self.title = title
        self.price = price
    def get_time_to_read(self):
        pass    
class Book:
    def __init__(self, title, price, pages):
        super().__init__(title, price)
        self.pages = pages
    def get_info(self):
        return f"Kniha '{self.title}' má {self.pages} stran a stojí {self.price} Kč."
    def get_time_to_read(self):
        return self.pages * 4 / 60
class AudioBook:
    def __init__(self, title, price, duration_in_hours, narrator):
        super().__init__(title, price)
        self.duration_in_hours = duration_in_hours
        self.narrator = narrator
    def get_time_to_read(self):
        return self.duration_in_hours
book_1 = Book("Kadet Hornblower", 399, 242)
audiobook_1 = AudioBook("Problém tří těles", 299, 14.4, "Zbyšek Horák")
```