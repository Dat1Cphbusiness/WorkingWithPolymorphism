# Level 2: Assignments – Abstrakte Klasser

---

### Opgave 2.1: Abstrakt superklasse
Lav den abstrakte klasse `Dyr` med feltet `navn` (String), en konstruktør og den abstrakte metode `void lavLyd()`.

Lav to konkrete subklasser: `Hund` der printer `Vuf!` og `Fugl` der printer `Tweet!`.

Opret én af hver i `main` og kald `lavLyd()`.

<details>
<summary>Hint</summary>

`abstract class Dyr` og `abstract void lavLyd()` – ingen krop på metoden i superklassen.
</details>

<details>
<summary>Se svar</summary>

```java
abstract class Dyr {
    String navn;

    Dyr(String navn) {
        this.navn = navn;
    }

    abstract void lavLyd();
}

class Hund extends Dyr {
    Hund(String navn) { super(navn); }

    @Override
    void lavLyd() {
        System.out.println(navn + " siger: Vuf!");
    }
}

class Fugl extends Dyr {
    Fugl(String navn) { super(navn); }

    @Override
    void lavLyd() {
        System.out.println(navn + " siger: Tweet!");
    }
}

void main() {
    Hund h = new Hund("Rex");
    Fugl f = new Fugl("Tweety");
    h.lavLyd();
    f.lavLyd();
}
```
</details>

---

### Opgave 2.2: Konkret metode i abstrakt klasse
Udvid `Dyr` fra opgave 2.1 med en **konkret** metode `void præsenter()` der printer `Jeg hedder [navn]` og derefter kalder `lavLyd()`.

Kald `præsenter()` på en `Hund` og en `Fugl` og se at den rigtige lyd bruges automatisk.

<details>
<summary>Se svar</summary>

```java
abstract class Dyr {
    String navn;

    Dyr(String navn) {
        this.navn = navn;
    }

    abstract void lavLyd();

    void præsenter() {
        System.out.println("Jeg hedder " + navn);
        lavLyd();
    }
}
```

Ingen ændringer i `Hund` og `Fugl` – de arver `præsenter()` automatisk.
</details>

---

### Opgave 2.3: Kan du instansiere en abstrakt klasse?
Prøv at skrive `Dyr d = new Dyr("x");` i `main`.  
Hvad sker der, og hvorfor?

Skriv svaret som en kommentar i din kode.

<details>
<summary>Se svar</summary>

Du får en **kompileringsfejl**: `Dyr is abstract; cannot be instantiated`.

Det er præcis meningen – en abstrakt klasse definerer en skabelon, men det giver ikke mening at oprette et "generisk dyr" uden konkret adfærd.
</details>

---

### Opgave 2.4: Figurer med fælles adfærd
Lav den abstrakte klasse `Figur` med:
- Feltet `farve` (String)
- Konstruktør
- Abstrakt metode `double getAreal()`
- Konkret metode `void printInfo()` der printer farven og arealet

Lav to subklasser: `Kvadrat` (felt: `side`) og `Trekant` (felter: `grundlinje`, `højde`).  
Formlerne: kvadrat = side², trekant = (grundlinje × højde) / 2.

<details>
<summary>Se svar</summary>

```java
abstract class Figur {
    String farve;

    Figur(String farve) {
        this.farve = farve;
    }

    abstract double getAreal();

    void printInfo() {
        System.out.println("Farve: " + farve + ", Areal: " + getAreal());
    }
}

class Kvadrat extends Figur {
    double side;

    Kvadrat(String farve, double side) {
        super(farve);
        this.side = side;
    }

    @Override
    double getAreal() {
        return side * side;
    }
}

class Trekant extends Figur {
    double grundlinje, højde;

    Trekant(String farve, double grundlinje, double højde) {
        super(farve);
        this.grundlinje = grundlinje;
        this.højde = højde;
    }

    @Override
    double getAreal() {
        return (grundlinje * højde) / 2;
    }
}

void main() {
    Kvadrat k = new Kvadrat("blå", 4.0);
    Trekant t = new Trekant("rød", 6.0, 3.0);
    k.printInfo();
    t.printInfo();
}
```
</details>
