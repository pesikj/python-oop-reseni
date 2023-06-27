# Abstraktní třída

## Jízdenky a letenky

Nyní je naším cílem práce pro společnost, která se zabývá prodejem jízdenek a letenek. Uvažujeme možnost koupit si lístek na vlak a letenku.

- Vytvoř abstraktní třídu `Ticket`, která bude mít atributy `basic_price` (základní cena bez služeb) a `fare_class` (třída, kterou cestující letí, uvažujeme možnosti `economy` a `business`). Dále vytvoř abstraktní metodu `total_price()` (celková cena).
- Vytvoř třídu `TrainTicket`, která bude dědit od abstraktní třídy `Ticket`. Naprogramuj metodu `total_price()`, která bude vracet hodnotu stejnou jako `basic_price`, pokud atribut `fare_class` je `economy`, a cenu o 20 % vyšší oproti `basic_price`, pokud `fare_class` je `business`.
- Dále vytvoř třídu `PlaneTicket`, která bude mít navíc atribut `checkout_luggages`, který udává počet odbavených zavazadel. Naprogramuj metodu `total_price()`, která bude vracet hodnotu stejnou jako `basic_price`, pokud atribut `fare_class` je `economy`, a cenu o 50 % vyšší oproti `basic_price`, pokud `fare_class` je `business`. Dále připočti 2000 za každé odbavené zavazadlo (bez ohledu na třídu).
- Zkus vytvořit objekt na základě třídy `Ticket`. Vidíš podobnou chybu, jaká byla v lekci?
- Vytvoř jízdenku na vlak se základní cenou 150 do tříd `economy` i `business`. Zkontroluj, jakou hodnotu vrací metoda `total_price()`.
- Vytvoř letenku se základní cenou 6000 do tříd `economy` i `business` s jedním odbaveným zavazadlem. Zkontroluj, jakou hodnotu vrací metoda `total_price()`.

```py
from abc import ABC, abstractmethod

class Ticket(ABC):
    def __init__(self, basic_price, fare_class):
        self.basic_price = basic_price
        self.fare_class = fare_class

    @abstractmethod
    def total_price(self):
        pass


class TrainTicket(Ticket):
    def total_price(self):
        if self.fare_class == 'economy':
            return self.basic_price
        elif self.fare_class == 'business':
            return self.basic_price * 1.2


class PlaneTicket(Ticket):
    def __init__(self, basic_price, fare_class, checkout_luggages):
        super().__init__(basic_price, fare_class)
        self.checkout_luggages = checkout_luggages

    def total_price(self):
        luggage_price = self.checkout_luggages * 2000
        if self.fare_class == 'economy':
            return self.basic_price + luggage_price
        elif self.fare_class == 'business':
            return self.basic_price * 1.5 + luggage_price

# Vytvoření objektu z abstraktní třídy skončí chybou:
# ticket = Ticket(1000, 'economy')  # TypeError: Can't instantiate abstract class Ticket with abstract methods total_price

train_ticket_economy = TrainTicket(150, 'economy')
train_ticket_business = TrainTicket(150, 'business')
print(train_ticket_economy.total_price())  # 150
print(train_ticket_business.total_price())  # 180

plane_ticket_economy = PlaneTicket(6000, 'economy', 1)
plane_ticket_business = PlaneTicket(6000, 'business', 1)
print(plane_ticket_economy.total_price())  # 8000
print(plane_ticket_business.total_price())  # 11000
```
