# Level 2: Abstrakte Klasser

## Problemet abstrakte klasser løser

Forestil dig du har en superklasse `Form` med metoden `getAreal()`. Men hvad skal `Form.getAreal()` returnere? En generisk form har ikke et areal – kun konkrete former som `Cirkel` og `Rektangel` har det.

Løsningen: gør `Form` **abstrakt**.

---

## abstract class

En abstrakt klasse kan **ikke instansieres** direkte:

```java
abstract class Form {
    String farve;

    Form(String farve) {
        this.farve = farve;
    }
}
```

```java
Form f = new Form("rød");  // FEJL – abstrakt klasse kan ikke instansieres
Cirkel c = new Cirkel("rød", 5.0);  // OK
```

Du bruger abstrakte klasser til at definere **fælles struktur** for en gruppe af klasser, uden at det giver mening at oprette selve superklassen.

---

## abstract metode

En abstrakt metode har **ingen krop** – kun en signatur:

```java
abstract class Form {
    String farve;

    abstract double getAreal();  // Ingen krop – subklassen SKAL implementere den
}
```

Alle konkrete subklasser er **tvunget** til at implementere abstrakte metoder:

```java
class Cirkel extends Form {
    double radius;

    Cirkel(String farve, double radius) {
        super(farve);
        this.radius = radius;
    }

    @Override
    double getAreal() {
        return Math.PI * radius * radius;
    }
}

class Rektangel extends Form {
    double bredde, højde;

    Rektangel(String farve, double bredde, double højde) {
        super(farve);
        this.bredde = bredde;
        this.højde = højde;
    }

    @Override
    double getAreal() {
        return bredde * højde;
    }
}
```

---

## Konkrete metoder i abstrakte klasser

En abstrakt klasse kan godt have **konkrete metoder** (med krop) der deles af alle subklasser:

```java
abstract class Form {
    String farve;

    abstract double getAreal();  // Abstrakt – skal overskrives

    void printInfo() {           // Konkret – arves direkte
        System.out.println("Farve: " + farve);
        System.out.println("Areal: " + getAreal());
    }
}
```

Her kalder `printInfo()` `getAreal()` – den korrekte version køres automatisk afhængig af hvilken subklasse objektet er.

---

## Hvornår abstrakt klasse?

Brug en abstrakt klasse når:
- Klasserne **deler felter og/eller konkrete metoder**
- Det **ikke giver mening** at oprette superklassen direkte
- Du vil **tvinge** subklasser til at implementere bestemte metoder

| | Abstrakt klasse | Konkret klasse |
|---|---|---|
| Kan instansieres | ❌ | ✅ |
| Kan have felter | ✅ | ✅ |
| Kan have konkrete metoder | ✅ | ✅ |
| Kan have abstrakte metoder | ✅ | ❌ |

---

## UML

Abstrakte klasser og metoder skrives i **kursiv** i UML:

```
     «abstract»
       Form
    ──────────
    farve
    ──────────
    getAreal()   ← kursiv = abstrakt
    printInfo()
         △
        / \
   Cirkel  Rektangel
```
