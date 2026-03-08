# Level 3: Assignments – Interfaces

---

### Opgave 3.1: Dit første interface
Definer interfacet `Greetable` med én metode: `String getHilsen()`.

Lav to klasser der implementerer det: `DanskPerson` der returnerer `Hej!` og `EngelskPerson` der returnerer `Hello!`.

Opret én af hver og print hilsenen.

<details>
<summary>Hint</summary>

`class DanskPerson implements Greetable` – husk `@Override` og at returnere en String.
</details>

<details>
<summary>Se svar</summary>

```java
interface Greetable {
    String getHilsen();
}

class DanskPerson implements Greetable {
    @Override
    String getHilsen() {
        return "Hej!";
    }
}

class EngelskPerson implements Greetable {
    @Override
    String getHilsen() {
        return "Hello!";
    }
}

void main() {
    DanskPerson d = new DanskPerson();
    EngelskPerson e = new EngelskPerson();
    System.out.println(d.getHilsen());
    System.out.println(e.getHilsen());
}
```
</details>

---

### Opgave 3.2: Hvad sker der hvis du glemmer en metode?
Lav interfacet `Regnbar` med to metoder: `double getAreal()` og `double getOmkreds()`.

Lav klassen `Cirkel` der implementerer `Regnbar`, men kun implementerer `getAreal()` – udelad `getOmkreds()` bevidst.

Hvad sker der, og hvad siger fejlbeskeden?

<details>
<summary>Se svar</summary>

Du får en kompileringsfejl – noget i retning af:  
`Cirkel is not abstract and does not override abstract method getOmkreds() in Regnbar`

En klasse **skal** implementere alle metoder fra et interface, medmindre klassen selv er abstrakt.
</details>

---

### Opgave 3.3: Flere interfaces
Definer to interfaces:
- `Svømmende` med metoden `void svøm()`
- `Flyvende` med metoden `void flyv()`

Lav klassen `And` der implementerer **begge**. Lav klassen `Fisk` der kun implementerer `Svømmende`.

Kald de relevante metoder i `main`.

<details>
<summary>Se svar</summary>

```java
interface Svømmende {
    void svøm();
}

interface Flyvende {
    void flyv();
}

class And implements Svømmende, Flyvende {
    @Override
    public void svøm() {
        System.out.println("Ællingen svømmer");
    }

    @Override
    public void flyv() {
        System.out.println("Ællingen flyver");
    }
}

class Fisk implements Svømmende {
    @Override
    public void svøm() {
        System.out.println("Fisken svømmer");
    }
}

void main() {
    And a = new And();
    Fisk f = new Fisk();
    a.svøm();
    a.flyv();
    f.svøm();
}
```
</details>

---

### Opgave 3.4: extends og implements
Lav den abstrakte klasse `Dyr` med feltet `navn` og en konstruktør.  
Lav interfacet `Tamme` med metoden `void kæl()`.  
Lav klassen `Hund` der **både** nedarver fra `Dyr` **og** implementerer `Tamme`.

<details>
<summary>Se svar</summary>

```java
abstract class Dyr {
    String navn;
    Dyr(String navn) { this.navn = navn; }
}

interface Tamme {
    void kæl();
}

class Hund extends Dyr implements Tamme {
    Hund(String navn) { super(navn); }

    @Override
    public void kæl() {
        System.out.println(navn + " logrer med halen");
    }
}

void main() {
    Hund h = new Hund("Rex");
    h.kæl();
}
```
</details>

---

### Opgave 3.5: Interface vs. abstrakt klasse
Svar på følgende i en kommentar i din kode:

1. Hvornår vil du vælge en **abstrakt klasse** frem for et interface?
2. Hvornår vil du vælge et **interface** frem for en abstrakt klasse?
3. Hvad er den praktiske forskel på de to i Java?

<details>
<summary>Se svar</summary>

1. **Abstrakt klasse** når klasserne deler felter eller konkrete metoder – fx alle `Dyr` har et `navn` og kan `præsenter()` sig.
2. **Interface** når urelaterede klasser skal have samme adfærd – fx både `And` og `Flyver` kan flyve, selvom de ikke er beslægtede.
3. En klasse kan kun arve fra **én** abstrakt klasse, men implementere **mange** interfaces.
</details>
