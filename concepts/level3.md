# Level 3: Interfaces

## Hvad er et interface?

Et interface er en **kontrakt**. Det siger: "enhver klasse der implementerer mig, lover at have disse metoder."

Et interface definerer **hvad** en klasse kan – ikke **hvordan** den gør det.

---

## Definer et interface

```java
interface Bevægelig {
    void bevægDig();
    int getHastighed();
}
```

- Metoderne har **ingen krop**
- Alle metoder er implicit `public`
- Et interface har ingen konstruktør og ingen felter (med få undtagelser)

---

## implements

En klasse implementerer et interface med `implements`:

```java
class Bil implements Bevægelig {
    @Override
    void bevægDig() {
        System.out.println("Bilen kører");
    }

    @Override
    int getHastighed() {
        return 120;
    }
}
```

Klassen **skal** implementere alle interfacets metoder – ellers giver compileren fejl.

---

## En klasse kan implementere flere interfaces

En klasse kan kun arve fra **én** superklasse, men kan implementere **mange** interfaces:

```java
interface Svømmende {
    void svøm();
}

interface Flyvende {
    void flyv();
}

class And implements Svømmende, Flyvende {
    @Override
    void svøm() {
        System.out.println("Ællingen svømmer");
    }

    @Override
    void flyv() {
        System.out.println("Ællingen flyver");
    }
}
```

---

## extends og implements samtidig

En klasse kan både arve og implementere:

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
    void kæl() {
        System.out.println(navn + " logrer med halen");
    }
}
```

---

## Interface vs. abstrakt klasse

| | Interface | Abstrakt klasse |
|---|---|---|
| Felter | ❌ (kun konstanter) | ✅ |
| Konstruktør | ❌ | ✅ |
| Konkrete metoder | ❌ (normalt) | ✅ |
| Multiple "arv" | ✅ (mange interfaces) | ❌ (én superklasse) |
| Brug når... | Klasser deler **adfærd** | Klasser deler **struktur og kode** |

**Tommelfingerregel:**
- Abstrakt klasse = fælles kode og felter
- Interface = fælles kontrakt på tværs af urelaterede klasser

---

## UML

Interfaces vises med `«interface»` og implementering med **stiplet pil**:

```
  «interface»
  Bevægelig
  ──────────
  bevægDig()
  getHastighed()
      ▲
    (stiplet)
      │
     Bil
```
