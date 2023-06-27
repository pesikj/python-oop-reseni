# Další metody

## Balík podruhé

Vrať se k návrhu software pro zásilkovou společnost.

- U třídy `Package` přejmenuj metodu `get_info()` na `__str__()` a vyzkoušej, jestli nyní stačí k získání informací o balíku funkce `print()`.
- Přidej metodu `deliver()`. Půjde o obdobu tlačítka, které řidič nebo řidička zmáčkne při doručení balíku a zaznamená tak jeho doručení. Metoda nejprve zkontroluje, zda balík náhodou již není ve stavu `doručen`. Pokud ano, metoda vrátí zprávu "Balík již byl doručen". Tím bude řidič (řidička) informován(a) o tom, že se pravděpodobně spletl(a) a snaží se zaznamenat doručení u špatného balíku. Pokud balík není ve stavu `doručen`, změň jeho stav právě na `doručen` a vrať zprávu "Doručení uloženo".
- Vyzkoušej metodu `deliver()`. Co se stane, pokud ji u jednoho balíku zavoláš dvakrát?

```py
class Package:
    def __init__(self, address, weight, state):
        self.address = address
        self.weight = weight
        self.state = state

    def __str__(self):
        return f"Balík na adresu {self.address} má hmotnost {self.weight} kg a je ve stavu {self.state}."

    def deliver(self):
        if self.state == "doručen":
            return "Balík již byl doručen"
        else:
            self.state = "doručen"
            return "Doručení uloženo"

# Vytvoření objektů
package1 = Package("Václavské Náměstí 12, Praha", 0.25, "nedoručen")
package2 = Package("Jiřího z Poděbrad 9, Brno", 1.5, "doručen")

# Výpis informací o balících
print(package1)
print(package2)

# Zkouška metody deliver
print(package1.deliver())
print(package1)  # Balík by měl být nyní ve stavu "doručen"
print(package1.deliver())  # Metoda by nyní měla vrátit zprávu, že balík již byl doručen
```

## Kniha podruhé

Vrať se k práci se třídou `Book`. Pokud jsi ji nestihl(a) v minulé části vytvořit, vrať se nejprve k zadání příkladu na předchozí stránce a třídu si vytvoř.

- U knihy budeme chtít evidovat, kolik kusů bylo prodáno. Přidej atribut `sold`, jehož hodnotu bude možné nastavit v metodě `__init__()`. Dále přidej atribut `costs`, které představují náklady na jednu knihu (např. tisk, doprava do knihkupectví, podíl autora (autorky) atd.).
- Přidej metodu `profit()`, která vrátí celkový zisk z knihy. Zisk vypočti na základě vzorce: prodané kusy * (cena - náklady).
- Přidej metodu `rating()`, která vrátí hodnocení knihy na základě jejího zisku. Pokud bude zisk méně než 50 tisíc, vrať hodnotu "propadák". Pokud bude zisk mezi 50 tisíc a 500 tisíc, vrať hodnotu "průměr". Pokud bude vyšší než 500 tisíc, vrať hodnotu "úspěch".

```py
class Book:
    def __init__(self, title, pages, price, sold, costs):
        self.title = title
        self.pages = pages
        self.price = price
        self.sold = sold
        self.costs = costs

    def get_info(self):
        return f"Kniha '{self.title}' má {self.pages} stran, stojí {self.price} Kč, bylo prodáno {self.sold} kusů a náklady na jednu knihu činí {self.costs} Kč."

    def get_time_to_read(self):
        return self.pages * 4 / 60

    def profit(self):
        return self.sold * (self.price - self.costs)

    def rating(self):
        profit = self.profit()
        if profit < 50000:
            return "propadák"
        elif profit <= 500000:
            return "průměr"
        else:
            return "úspěch"

# Vytvoření objektů
book1 = Book("Problém tří těles", 447, 250)
book2 = Book("Temný les", 600, 300)

# Výpis informací o knihách, zisku a hodnocení
print(book1.get_info())
print(f"Zisk: {book1.profit()} Kč, Hodnocení: {book1.rating()}")
print(book2.get_info())
print(f"Zisk: {book2.profit()} Kč, Hodnocení: {book2.rating()}")
```

## Zkušební doba

U zaměstnanců budeme nově evidovat, jestli jsou ve zkušební době.

- Rozšiř metodu `__init__` třídy `Zamestnanec` o parametr `zkusebni_doba`, který bude typu `bool`. Tuto hodnotu ulož jako atribut třídy `Zamestnanec`.
- Uprav metodu `__str__`. Pokud je zaměstnanec ve zkušební době, přidej k jeho/jejímu výpisu text `Je ve zkušební době.`

```py
class Employee:
    def __init__(self, name, position, holiday_entitlement, probation_period):
        self.name = name
        self.position = position
        self.holiday_entitlement = holiday_entitlement
        self.probation_period = probation_period

    def __str__(self):
        text = f"Zaměstnanec {self.name} pracuje na pozici {self.position}."
        if self.probation_period:
            text = text + " Je ve zkušební době."
        return text

    def take_holiday(self, days):
        if self.holiday_entitlement >= days:
            self.holiday_entitlement -= days
            return "Užij si to."
        else:
            return f"Bohužel už máš nárok jen na {self.holiday_entitlement} dní."

# Vytvoření objektů
employee1 = Employee("Jan Novák", "Programátor", 25, True)
employee2 = Employee("Marie Kovaříková", "HR Manager", 30, False)

# Výpis informací o zaměstnancích
print(employee1)
print(employee2)

```

