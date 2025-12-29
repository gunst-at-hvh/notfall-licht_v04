# Notfall-Licht Tutorial

```package
lichtsensor-events=github:gunst-at-hvh/pxt-lichtsensor-events
```

## Einführung @unplugged

Baue ein **Notfall-Licht**: Geht automatisch an wenn es dunkel wird!

Der **Lichtsensor** (oben links) misst die Helligkeit.

## Aufgabe 1 @unplugged

**Drücke** Knopf A → Zeigt die aktuelle Helligkeit

**Programmiere:** Speichere die Normal-Helligkeit

💡 Der Calliope lernt: "Das ist hell"

```template
input.onButtonPressed(Button.A, function () {
    basic.showNumber(lichtsensor.lichtwert())
})
```

## Schritt 1: Normal-Helligkeit speichern

Ziehe ``||lichtsensor:speichere Normal-Helligkeit||`` in ``||basic:beim Start||``.

<details>
<summary>💡 Tipp</summary>

Öffne ``||lichtsensor:Lichtsensor||`` → Ziehe ``||lichtsensor:speichere Normal-Helligkeit||`` in ``||basic:beim Start||`` → Trage Wert ein (z.B. 60).

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
```

**Normal-Helligkeit:** Wie hell es ist wenn Licht an ist | Werte: Heller Raum: 80-100 | Normal: 50-70 | Dunkel: 30-50

```validation.global
# BlocksExistValidator
* Enabled: true
```

## Aufgabe 2 @unplugged

**Verzweigung programmieren!**

Der Calliope weiss jetzt "hell".  
Alles dunkler = "dunkel".

**Verzweigung** = Zwei Wege:

```
     Calliope entscheidet
           ↙      ↘
      DUNKEL      HELL
    Licht AN   Licht AUS
```

💡 **Entweder**-**oder** - der Calliope wählt!

---

**Programmiere beide Wege:**

Wenn ``||lichtsensor:dunkel||`` → ``||basic:Matrix||`` AN

Wenn ``||lichtsensor:hell||`` → ``||basic:Matrix||`` + ``||basic:RGB||`` AUS

## Schritt 2: Ereignis "dunkel"

Ziehe ``||lichtsensor:wenn Licht dunkel||`` in den Arbeitsbereich.

<details>
<summary>💡 Tipp</summary>

Öffne ``||lichtsensor:Lichtsensor||`` → Ziehe ``||lichtsensor:wenn Licht dunkel||`` in den Arbeitsbereich (nicht in anderen Block!).

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    
})
```

**Ereignis** = reagiert automatisch (ohne Knopfdruck)

## Schritt 3: Matrix ein

Bei Dunkelheit: Alle LEDs an.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||basic:zeige LEDs||`` IN den ``||lichtsensor:wenn Licht dunkel||`` Block → Klicke alle Quadrate an.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
// @validate-exists
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showLeds(`
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        `)
})
```

**LED-Matrix** = 5x5 LEDs = Maximum Licht!

## Schritt 4: Ereignis "hell"

Ziehe ``||lichtsensor:wenn Licht||`` in den Arbeitsbereich, wähle ``hell``.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||lichtsensor:wenn Licht dunkel||`` → Klicke auf "dunkel" → Wähle "hell".

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showLeds(`
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        `)
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    
})
```

**Verzweigung:** Jetzt beide Wege programmiert! ✅

## Schritt 5: Matrix aus

Bei Helligkeit: Matrix leer.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||basic:zeige LEDs||`` IN den ``||lichtsensor:wenn Licht hell||`` Block → Lass alle Quadrate leer (nicht anklicken).

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showLeds(`
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        `)
})
// @validate-exists
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
```

**Test:** Lade auf Calliope → Hand über Sensor (oben links) → LEDs an!

## Schritt 6: RGB aus

Füge ``||basic:lösche RGB LED||`` in den wenn-hell Block ein.

<details>
<summary>💡 Tipp</summary>

Öffne ``||basic:Grundlagen||`` → Klicke ``||basic:... mehr||`` → Ziehe ``||basic:lösche RGB LED||`` IN ``||lichtsensor:wenn Licht hell||``.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showLeds(`
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        `)
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**Warum?** LEDs beeinflussen Sensor → Alles aus = bessere Messung!

```validation.local
# BlocksExistValidator
* Enabled: false
```

## Aufgabe 3 @unplugged

**Verbessern:**

Bei ``||lichtsensor:dunkel||`` → ``||basic:RGB rot||`` (Alarm!)

``||basic:Symbol||`` statt Matrix (z.B. Herz)

## Schritt 7: RGB rot

Füge ``||basic:setze LED Farbe rot||`` in den wenn-dunkel Block ein.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||basic:setze LED Farbe||`` IN ``||lichtsensor:wenn Licht dunkel||`` → Wähle rot.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
// @validate-exists
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showLeds(`
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        # # # # #
        `)
    basic.setLedColor(0xff0000)
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**Farben:** Rot (0xff0000) | Orange (0xff8000) | Gelb (0xffff00)

## Schritt 8: Symbol

Ersetze ``||basic:zeige LEDs||`` durch ``||basic:zeige Symbol||`` im wenn-dunkel Block.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||basic:zeige LEDs||`` raus (löschen) → Ziehe ``||basic:zeige Symbol||`` rein → Wähle Symbol.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    basic.showIcon(IconNames.Heart)
    basic.setLedColor(0xff0000)
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**Ideen:** Herz ❤️ | Sonne ☀️ | Blitz ⚡ | Eigenes!

## Aufgabe 4 (Profi!) @unplugged

**Blink-Sequenz:**

**Sequenz** = Mehrere Anweisungen hintereinander

**Schleife** = Wiederholt die Sequenz

→ Verschiedene ``||basic:Symbole||`` + ``||basic:Farben||`` + ``||basic:Pausen||``

## Schritt 9: Schleife

Füge eine **Schleife** ein um deine Animation zu wiederholen.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||loops:wiederhole 4 mal||`` IN ``||lichtsensor:wenn Licht dunkel||`` → Ziehe deine Blöcke (Symbol, Farbe) IN die Schleife.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    for (let index = 0; index < 4; index++) {
        basic.showIcon(IconNames.Heart)
        basic.setLedColor(0xff0000)
    }
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**Problem:** Keine Änderung → sieht aus wie 1x!

## Schritt 10: Änderungen

Füge Änderungen in die Schleife: Verschiedene Symbole, Farben, Pausen.

<details>
<summary>💡 Tipp</summary>

IN die Schleife: Symbol 1 → Farbe 1 → ``||basic:pausiere 100 ms||`` → Symbol 2 → Farbe 2 → ``||basic:pausiere 100 ms||``.

</details>

```blocks
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    for (let index = 0; index < 2; index++) {
        basic.showIcon(IconNames.Heart)
        basic.setLedColor(0xff0000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallHeart)
        basic.setLedColor(0x00ff00)
        basic.pause(100)
    }
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**Experimentiere:** Mehr Wiederholungen | Andere Symbole | Andere Farben | Mehr Schritte!

## Aufgabe 5 @unplugged

**Neu einstellen** (heißt auch: Kalibrierung)

Mit ``||input:Knopf B||``: Aktuellen ``||lichtsensor:Lichtwert||`` messen → Speichern → ``||basic:Häkchen||`` zeigen

💡 Hell-Wert an Raum anpassen!

## Schritt 11: Knopf B

Erstelle Ereignis für Knopf B.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||input:wenn Knopf A gedrückt||`` → Klicke auf "A" → Wähle "B".

</details>

```blocks
input.onButtonPressed(Button.B, function () {
    
})
```

## Schritt 12: Neu einstellen

Füge Neu-Einstellen-Logik in Knopf B ein.

<details>
<summary>💡 Tipp</summary>

Ziehe ``||lichtsensor:speichere Normal-Helligkeit||`` IN Knopf B → Ziehe ``||lichtsensor:Lichtwert||`` ins Zahlenfeld! → Füge ``||basic:zeige Symbol Häkchen||`` hinzu.

</details>

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showNumber(lichtsensor.lichtwert())
})
input.onButtonPressed(Button.B, function () {
    lichtsensor.setzeReferenzlicht(lichtsensor.lichtwert())
    basic.showIcon(IconNames.Yes)
})
lichtsensor.setzeReferenzlicht(60)
lichtsensor.wennLichtWechselt(LichtZustand.Dunkel, function () {
    for (let index = 0; index < 2; index++) {
        basic.showIcon(IconNames.Heart)
        basic.setLedColor(0xff0000)
        basic.pause(100)
        basic.showIcon(IconNames.SmallHeart)
        basic.setLedColor(0x00ff00)
        basic.pause(100)
    }
})
lichtsensor.wennLichtWechselt(LichtZustand.Hell, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.turnRgbLedOff()
})
```

**So nutzen:** Calliope aufstellen → Normale Helligkeit abwarten → Knopf B → Häkchen ✅

## Fertig! @unplugged

🎉 **Fertig!**

**Gelernt:**

✅ **Verzweigung** (entweder dunkel oder hell)

✅ **Sequenz** (Anweisungen hintereinander)

✅ **Schleife** (wiederholt Sequenz)

**Teste:** Verschiedene Räume | Mit Knopf B anpassen

<script src="https://makecode.com/gh-pages-embed.js"></script>
<script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>


> Diese Seite bei [https://gunst-at-hvh.github.io/notfall-licht_v04/](https://gunst-at-hvh.github.io/notfall-licht_v04/) öffnen

## Als Erweiterung verwenden

Dieses Repository kann als **Erweiterung** in MakeCode hinzugefügt werden.

* öffne [https://makecode.calliope.cc/](https://makecode.calliope.cc/)
* klicke auf **Neues Projekt**
* klicke auf **Erweiterungen** unter dem Zahnrad-Menü
* nach **https://github.com/gunst-at-hvh/notfall-licht_v04** suchen und importieren

## Dieses Projekt bearbeiten

Um dieses Repository in MakeCode zu bearbeiten.

* öffne [https://makecode.calliope.cc/](https://makecode.calliope.cc/)
* klicke auf **Importieren** und dann auf **Importiere URL**
* füge **https://github.com/gunst-at-hvh/notfall-licht_v04** ein und klicke auf Importieren

#### Metadaten (verwendet für Suche, Rendering)

* for PXT/calliopemini
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
