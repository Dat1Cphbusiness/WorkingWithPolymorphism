# Level 1: Assignments – Nedarving

---

### Opgave 1.1: Din første subklasse
Lav klassen `Køretøj` med felterne `mærke` (String) og `hastighed` (int), en konstruktør og metoden `void beskriv()` der printer begge felter.

Lav derefter klassen `Bil` der nedarver fra `Køretøj` og tilføjer feltet `antalDøre` (int).

Opret en `Bil` i `main` og kald `beskriv()`.

<details>
<summary>Hint</summary>

Brug `extends`. `Bil` arver automatisk `mærke`, `hastighed` og `beskriv()`.
</details>

<details>
<summary>Se svar</summary>

```java
class Køretøj {
    String mærke;
    int hastighed;

    Køretøj(String mærke, int hastighed) {
        this.mærke = mærke;
        this.hastighed = hastighed;
    }

    void beskriv() {
        System.out.println(mærke + " – " + hastighed + " km/t");
    }
}

class Bil extends Køretøj {
    int antalDøre;

    Bil(String mærke, int hastighed, int antalDøre) {
        super(mærke, hastighed);
        this.antalDøre = antalDøre;
    }
}

void main() {
    Bil b = new Bil("Toyota", 180, 4);
    b.beskriv();
    System.out.println("Døre: " + b.antalDøre);
}
```
</details>

---

### Opgave 1.2: Override
Udvid opgave 1.1. Lav klassen `Motorcykel` der også nedarver fra `Køretøj`, men **overskriver** `beskriv()` så den printer noget andet end Køretøj's version – fx med en motorcykel-emoji eller en anden tekst.

Opret én `Bil` og én `Motorcykel` og kald `beskriv()` på begge.

<details>
<summary>Se svar</summary>

```java
class Motorcykel extends Køretøj {
    Motorcykel(String mærke, int hastighed) {
        super(mærke, hastighed);
    }

    @Override
    void beskriv() {
        System.out.println("🏍 " + mærke + " – " + hastighed + " km/t");
    }
}

void main() {
    Bil b = new Bil("Toyota", 180, 4);
    Motorcykel m = new Motorcykel("Harley", 200);
    b.beskriv();
    m.beskriv();
}
```
</details>

---

### Opgave 1.3: super i en metode
Lav klassen `Person` med feltet `navn` og metoden `void præsenter()` der printer `Jeg hedder [navn]`.

Lav subklassen `Studerende` med feltet `studie` der **udvider** `præsenter()` ved at kalde `super.præsenter()` og derefter printe `Jeg læser [studie]`.

<details>
<summary>Se svar</summary>

```java
class Person {
    String navn;

    Person(String navn) {
        this.navn = navn;
    }

    void præsenter() {
        System.out.println("Jeg hedder " + navn);
    }
}

class Studerende extends Person {
    String studie;

    Studerende(String navn, String studie) {
        super(navn);
        this.studie = studie;
    }

    @Override
    void præsenter() {
        super.præsenter();
        System.out.println("Jeg læser " + studie);
    }
}

void main() {
    Studerende s = new Studerende("Anna", "Datamatiker");
    s.præsenter();
}
```
</details>

---

### Opgave 1.4: instanceof
Lav en `ArrayList<Person>` og tilføj en blanding af `Person`- og `Studerende`-objekter.  
Loop igennem listen og brug `instanceof` til kun at printe studiet for dem der er `Studerende`.

<details>
<summary>Hint</summary>

`if (p instanceof Studerende)` – husk at downcaste bagefter så du kan tilgå `studie`-feltet.
</details>

<details>
<summary>Se svar</summary>

```java
void main() {
    ArrayList<Person> personer = new ArrayList<>();
    personer.add(new Person("Mikkel"));
    personer.add(new Studerende("Anna", "Datamatiker"));
    personer.add(new Person("Lars"));
    personer.add(new Studerende("Sofie", "Multimediedesign"));

    for (int i = 0; i < personer.size(); i++) {
        Person p = personer.get(i);
        if (p instanceof Studerende) {
            Studerende s = (Studerende) p;
            System.out.println(s.navn + " læser " + s.studie);
        }
    }
}
```
</details>

---

### Opgave 1.5: Hvad printer dette?
Gæt output før du kører koden.

```java
class A {
    void hej() {
        System.out.println("Hej fra A");
    }
}

class B extends A {
    @Override
    void hej() {
        super.hej();
        System.out.println("Hej fra B");
    }
}

class C extends B {
    @Override
    void hej() {
        super.hej();
        System.out.println("Hej fra C");
    }
}

void main() {
    C c = new C();
    c.hej();
}
```

<details>
<summary>Se svar</summary>

```
Hej fra A
Hej fra B
Hej fra C
```

`C.hej()` kalder `super.hej()` som er `B.hej()`, der igen kalder `super.hej()` som er `A.hej()`. Kæden ruller fra bunden op.
</details>
