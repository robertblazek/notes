---
attachments: [Clipboard_2021-02-12-09-45-17.png, Clipboard_2021-02-12-09-51-50.png, Clipboard_2021-02-12-09-55-31.png, Clipboard_2021-02-12-09-57-50.png, "Snímek obrazovky 2021-02-12 v\_9.21.45.png"]
tags: [random]
title: Tvorba webových stránek v HTML
created: '2021-02-12T08:31:39.997Z'
modified: '2021-02-26T08:24:02.664Z'
---

# Tvorba webových stránek v HTML
## Vytvoření HTML souboru (zdrojový kód)
<details closed>
  <summary>Windows</summary>
  <markdown>
  [https://www.jakpsatweb.cz/jak-udelat.html](https://www.jakpsatweb.cz/jak-udelat.html)
  </markdown>
</details>

<details closed>
  <summary>Mac</summary>
  <markdown>
  <kbd>⌘</kbd>+<kbd>space</kbd>
Otevřít `TextEdit.app`
![](@attachment/Clipboard_2021-02-12-09-45-17.png)

"Nový dokument"
![](@attachment/Clipboard_2021-02-12-09-51-50.png)

Soubor → Uložit... (<kbd>⌘</kbd>+<kbd>S</kbd>)
![](@attachment/Clipboard_2021-02-12-09-55-31.png)

Vybrat složku, uložit jako HTML
![](@attachment/Clipboard_2021-02-12-09-57-50.png)
  </markdown>
</details>

## základ kódu
```html
<!doctype html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <title>Jazyk HTML</title>
</head>
<body>
    Tvorba WWW stránek
    ěščřžýáíé
</body>
</html>
```

## nějaké formátování
```html
<!doctype html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <title>Jazyk HTML</title>
</head>
<body>
    <h1>Tvorba www stránek</h1><br>

<div style="text-align: center;">
    <h2>Mraveneček</h2>
        <p>Polámal se mraveneček,<br>
        ví to celá obora, <br>
        o půlnoci zavolali <br>
        mravenčího doktora.</p>
        <p>Doktor klepe na srdíčko, <br>
        potom píše recepis: <br>
        třikrát denně prášek cukru <br>
        bude chlapík jako rys.</p>
</div>
    
    
        Jméno        Příjmení    Bydliště
        Jana        Krásná        Chrudim
        Petr        Kudrnka        Pardubice
        Helena        Musílková    Chrudim
    
<p style="text-align: justify"> citace, která se původně používala pro delší kusy citací. Zobrazuje se jako odstavec s větším levým a pravým odsazením (odsazení znamená, že je po okrajích odstavce prázdné místo). Díky odsazení se tag v praxi používá ani ne tak pro citaci, jako spíše pro odsazení. V dnešních prohlížečích je odsazení zpravidla 40 pixelů. Odsazení se zvětší, pokud se tag použije vícekrát za sebou.</p>
</body>
</html>```
