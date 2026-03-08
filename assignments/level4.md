# Level 4: Assignments – Polymorfi og Dynamic Binding

---

### Opgave 4.1: Reference vs. objekt
Lav klassen `Dyr` med metoden `void lavLyd()` der printer `...`.  
Lav `Hund` og `Kat` der begge overskriver `lavLyd()`.

Skriv derefter i `main`:
```java
Dyr d = new Hund();
d.lavLyd();
```

Hvilken `lavLyd()` kører – `Dyr`'s eller `Hund`'s? Skriv svaret som en kommentar.

<details>
<summary>Se svar</summary>

```java
class Dyr {
    void lavLyd() { System.out.println("..."); }
}

class Hund extends Dyr {
    @Override
    void lavLyd() { System.out.println("Vuf!"); }
}

class Kat extends Dyr {
    @Override
    void lavLyd() { System.out.println("Miau!"); }
}

void main() {
    Dyr d = new Hund();
    d.lavLyd();  // Printer "Vuf!" – objektet er en Hund, ikke et Dyr
}
```

Det er **objektets type** der bestemmer hvilken metode der kører – det er dynamic binding.
</details>

---

### Opgave 4.2: ArrayList med supertype
Lav en `ArrayList<Dyr>` og tilføj mindst to `Hund`- og to `Kat`-objekter i vilkårlig rækkefølge.  
Loop igennem listen og kald `lavLyd()` på hvert element.

<details>
<summary>Se svar</summary>

```java
void main() {
    ArrayList<Dyr> dyr = new ArrayList<>();
    dyr.add(new Hund());
    dyr.add(new Kat());
    dyr.add(new Hund());
    dyr.add(new Kat());

    for (int i = 0; i < dyr.size(); i++) {
        dyr.get(i).lavLyd();
    }
}
// Output:
// Vuf!
// Miau!
// Vuf!
// Miau!
```
</details>

---

### Opgave 4.3: Polymorfi med interface
Lav interfacet `Spillelig` med metoden `void afspil()`.  
Lav klasserne `Sang` og `Podcast` der begge implementerer `Spillelig` på hver sin måde.

Opret en `ArrayList<Spillelig>` med en blanding, og kald `afspil()` på alle elementer.

<details>
<summary>Se svar</summary>

```java
interface Spillelig {
    void afspil();
}

class Sang implements Spillelig {
    String titel;
    Sang(String titel) { this.titel = titel; }

    @Override
    public void afspil() {
        System.out.println("♪ Spiller: " + titel);
    }
}

class Podcast implements Spillelig {
    String navn;
    Podcast(String navn) { this.navn = navn; }

    @Override
    public void afspil() {
        System.out.println("🎙 Podcast: " + navn);
    }
}

void main() {
    ArrayList<Spillelig> playlist = new ArrayList<>();
    playlist.add(new Sang("Comfortably Numb"));
    playlist.add(new Podcast("Lex Fridman #400"));
    playlist.add(new Sang("Back in Black"));

    for (int i = 0; i < playlist.size(); i++) {
        playlist.get(i).afspil();
    }
}
```
</details>

---

### Opgave 4.4: Downcast med instanceof
Brug `ArrayList<Dyr>` fra opgave 4.2. Udvid loopet så det:
- Kalder `lavLyd()` på alle
- Kun for `Hund`-objekter: printer en ekstra linje `[logrer med halen]`

Brug `instanceof` og downcast.

<details>
<summary>Se svar</summary>

```java
for (int i = 0; i < dyr.size(); i++) {
    dyr.get(i).lavLyd();
    if (dyr.get(i) instanceof Hund) {
        Hund h = (Hund) dyr.get(i);
        System.out.println("[logrer med halen]");
    }
}
```
</details>

---

### Opgave 4.5: Hvad printer dette?
Gæt output før du kører koden.

```java
abstract class Form {
    abstract String getNavn();

    void print() {
        System.out.println("Jeg er en " + getNavn());
    }
}

class Cirkel extends Form {
    @Override
    String getNavn() { return "cirkel"; }
}

class Kvadrat extends Form {
    @Override
    String getNavn() { return "kvadrat"; }
}

void main() {
    ArrayList<Form> figurer = new ArrayList<>();
    figurer.add(new Cirkel());
    figurer.add(new Kvadrat());
    figurer.add(new Cirkel());

    for (int i = 0; i < figurer.size(); i++) {
        figurer.get(i).print();
    }
}
```

<details>
<summary>Se svar</summary>

```
Jeg er en cirkel
Jeg er en kvadrat
Jeg er en cirkel
```

`print()` er defineret i `Form` og kalder `getNavn()` – men dynamic binding sørger for at den rigtige version af `getNavn()` køres for hvert objekt.
</details>
