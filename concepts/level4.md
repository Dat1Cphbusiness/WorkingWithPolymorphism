# Level 4: Polymorfi og Dynamic Binding

## Hvad er polymorfi?

Polymorfi betyder "mange former". I Java betyder det at du kan **behandle objekter af forskellige typer ens**, så længe de deler en fælles supertype.

En maler behøver ikke vide om det er en cirkel eller et rektangel – han kalder bare `getAreal()`. Det er polymorfi i praksis.

---

## Reference vs. objekt

Du kan gemme et objekt i en variabel af **superklassens type**:

```java
Dyr d = new Hund();  // Reference er Dyr, objekt er Hund
```

- **Referencens type** (`Dyr`) bestemmer hvad compileren tillader dig at kalde
- **Objektets type** (`Hund`) bestemmer hvilken metode der faktisk kører

---

## Dynamic binding

Når du kalder en overskrevet metode, kører **objektets version** – ikke referencens:

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
    Dyr d1 = new Hund();
    Dyr d2 = new Kat();

    d1.lavLyd();  // Vuf!  – objektet er en Hund
    d2.lavLyd();  // Miau! – objektet er en Kat
}
```

Java afgør hvilken metode der køres **ved kørsel** (ikke ved kompilering). Det kaldes dynamic binding.

---

## ArrayList med supertype

Polymorfi bliver kraftfuldt når du samler objekter af forskellige typer i én liste:

```java
ArrayList<Dyr> dyr = new ArrayList<>();
dyr.add(new Hund());
dyr.add(new Kat());
dyr.add(new Hund());

for (int i = 0; i < dyr.size(); i++) {
    dyr.get(i).lavLyd();  // Korrekt metode køres for hvert objekt
}
```

**Output:**
```
Vuf!
Miau!
Vuf!
```

Det samme virker med interfaces:

```java
ArrayList<Shape> figurer = new ArrayList<>();
figurer.add(new Cirkel(5.0));
figurer.add(new Rektangel(3.0, 4.0));

for (int i = 0; i < figurer.size(); i++) {
    System.out.println(figurer.get(i).getAreal());
}
```

---

## Downcast

En reference af supertypen kan **ikke** kalde subklassens egne metoder:

```java
Dyr d = new Hund();
d.bjæf();  // FEJL – Dyr kender ikke bjæf()
```

Hvis du ved at objektet faktisk er en `Hund`, kan du **downcaste**:

```java
Dyr d = new Hund();
Hund h = (Hund) d;  // Downcast
h.bjæf();           // Nu virker det
```

Brug `instanceof` for at tjekke typen inden du caster:

```java
if (d instanceof Hund) {
    Hund h = (Hund) d;
    h.bjæf();
}
```

Hvis du caster forkert (`(Hund) new Kat()`), får du en `ClassCastException` ved kørsel.

---

## Polymorfi med interfaces

Polymorfi virker præcis det samme med interfaces:

```java
interface Spillelig {
    void afspil();
}

class Sang implements Spillelig {
    public void afspil() { System.out.println("♪ Spiller sang"); }
}

class Podcast implements Spillelig {
    public void afspil() { System.out.println("🎙 Spiller podcast"); }
}

void main() {
    ArrayList<Spillelig> playlist = new ArrayList<>();
    playlist.add(new Sang());
    playlist.add(new Podcast());
    playlist.add(new Sang());

    for (int i = 0; i < playlist.size(); i++) {
        playlist.get(i).afspil();
    }
}
```

---

## Opsummering

| Begreb | Hvad det er |
|--------|-------------|
| Polymorfi | Behandle objekter af forskellig type ens via fælles supertype |
| Dynamic binding | Objektets type bestemmer hvilken metode der kører |
| Downcast | Konvertere en supertype-reference til subtype for at få adgang til subklassens metoder |
| `instanceof` | Tjek objektets faktiske type inden downcast |
