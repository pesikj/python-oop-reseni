# Objekty a třídy

## Balík

Uvažuj, že navrhuješ software pro zásilkovou společnost.

- Vytvoř třídu `Package`, která bude mít tři atributy - `address`, `weight` a `state`. Vytvoř metodu `__init__`, která uloží hodnoty parametrů metody do atributů.
- Přidej metodu `get_info()`, která vrátí informace o balíku jako řetězec. Uvažuj například větu "Balík na adresu Václavské Náměstí 12, Praha má hmotnost 0.25 kg je je ve stavu nedoručen".
- Zkus si vytvořit alespoň dva objekty ze třídy `Balik`. U `address` uvažujeme typ řetězec (`str`), u `weight` desetinné číslo. U atributu `state` zadávej pro zjednodušení pouze dva stavy: `doručen` a `nedoručen`.
- Vypiš informace, které generuje metoda `get_info()`, na obrazovku, a ověř, že je vše v pořádku.

```py
class Package:
    def __init__(self, address, weight, state):
        self.address = address
        self.weight = weight
        self.state = state

    def get_info(self):
        return f"Balík na adresu {self.address} má hmotnost {self.weight} kg a je ve stavu {self.state}."

# Vytvoření objektů
package1 = Package("Václavské Náměstí 12, Praha", 0.25, "nedoručen")
package2 = Package("Jiřího z Poděbrad 9, Brno", 1.5, "doručen")

# Výpis informací o balících
print(package1.get_info())
print(package2.get_info())
```

## Kniha

Zkus pro nakladatelství vytvořit software s využitím tříd a objektů. Vytvoř tedy třídu `Book`, která reprezentuje knihu. Každá kniha bude mít atributy `title`, `pages` a `price`. Hodnoty nastav ve funkci `__init__`.

- Přidej knize funkci `get_info()`, která vypíše informace o knize v nějakém pěkném formátu.
- Přidej metodu `get_time_to_read()`. Metoda vrátí čas potřebný na přečtení knihy v hodinách. S využitím atributu `pages` vypočítej čas na přečtení knihy, přičemž uvažuj, že přečtení jedné stránky zabere průměrnému čtenáři/čtenářce 4 minuty.


```py
class Book:
    def __init__(self, title, pages, price):
        self.title = title
        self.pages = pages
        self.price = price

    def get_info(self):
        return f"Kniha '{self.title}' má {self.pages} stran a stojí {self.price} Kč."

    def get_time_to_read(self):
        # Přečtení jedné stránky trvá průměrně 4 minuty, takže celkový čas na přečtení knihy
        # je počet stran krát 4 minuty. Protože výsledek chceme ve hodinách, dělíme celkový počet minut 60.
        return self.pages * 4 / 60

# Vytvoření objektů
book1 = Book("Problém tří těles", 447, 250)
book2 = Book("Temný les", 600, 300)

# Výpis informací o knihách a času potřebného na jejich přečtení
print(book1.get_info())
print(f"Čas potřebný na přečtení: {book1.get_time_to_read()} hodin")
print(book2.get_info())
print(f"Čas potřebný na přečtení: {book2.get_time_to_read()} hodin")
```
