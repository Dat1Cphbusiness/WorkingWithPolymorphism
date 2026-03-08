# Level 1: Nedarving

## Hvad er nedarving?

Nedarving betyder at én klasse **arver** felter og metoder fra en anden klasse.

Tænk på det som en is-a relation:
- En `Hund` **er en** `Dyr`
- En `Bil` **er et** `Køretøj`
- En `Studerende` **er en** `Person`

Den klasse der arver kaldes en **subklasse**. Den klasse der arves fra kaldes en **superklasse**.

---

## extends

Du bruger nøgleordet `extends` til at arve:

```java
class Dyr {
    String navn;
    int energi;

    void spis() {
        System.out.println(navn + " spiser");
    }
}

class Hund extends Dyr {
    void bjæf() {
        System.out.println(navn + " siger: Vuf!");
    }
}
```

`Hund` arver `navn`, `energi` og `spis()` fra `Dyr` – og tilføjer sin egen metode `bjæf()`.

```java
void main() {
    Hund h = new Hund();
    h.navn = "Rex";
    h.spis();   // Arvet fra Dyr
    h.bjæf();   // Hundens egen metode
}
```

---

## super – kald superklassens konstruktør

Når subklassen har en konstruktør, skal den kalde superklassens konstruktør med `super()`:

```java
class Dyr {
    String navn;

    Dyr(String navn) {
        this.navn = navn;
    }
}

class Kat extends Dyr {
    String farve;

    Kat(String navn, String farve) {
        super(navn);         // Kalder Dyr's konstruktør
        this.farve = farve;
    }
}
```

`super()` skal altid være den **første linje** i subklassens konstruktør.

---

## @Override – overskrive en metode

En subklasse kan **overskrive** en metode fra superklassen:

```java
class Dyr {
    void lavLyd() {
        System.out.println("...");
    }
}

class Ko extends Dyr {
    @Override
    void lavLyd() {
        System.out.println("Muh!");
    }
}
```

`@Override` er ikke påkrævet, men anbefales – det fortæller compileren at du bevidst overskriver, og den fanger stavefejl i metodenavnet.

---

## super – kald superklassens metode

Du kan også kalde superklassens version af en metode med `super.metodenavn()`:

```java
class Dyr {
    void beskriv() {
        System.out.println("Jeg er et dyr");
    }
}

class Hund extends Dyr {
    @Override
    void beskriv() {
        super.beskriv();                    // Kalder Dyr's beskriv()
        System.out.println("Jeg er en hund");
    }
}
```

**Output:**
```
Jeg er et dyr
Jeg er en hund
```

---

## instanceof

Du kan tjekke om et objekt er en bestemt type med `instanceof`:

```java
Hund h = new Hund();
System.out.println(h instanceof Hund);  // true
System.out.println(h instanceof Dyr);   // true – en Hund er også et Dyr
```

---

## UML: is-a relationen

I et klassediagram vises nedarving med en **pil med hult trekantspids** fra subklassen mod superklassen:

```
        Dyr
         △
        /|\
       / | \
    Hund Ko  Kat
```

Læs pilen som: "Hund **er en** Dyr".
