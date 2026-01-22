# Kostky (PHP)
Obsahem cvičení je pomocí klonování repozitáře z GitHubu "stáhnout" kostru programu a dopsat skript.

Živá ukázka: <a href="https://php.edumach.cz/kostky.php" target="_blank">https://php.edumach.cz/kostky.php</a>.

## Příprava

1. Přihlas se **v terminálu** na server TuX.
2. Zapiš si v Gitu své údaje:
   ```
   $ git config --global user.name "Jméno Příjmení"
   $ git config --global user.email "10XPrijmeniJ@student.panska.cz"
   ``` 
3. Přesuň se do adresáře `~/www` a naklonuj repozitář `https://github.com/edumach/kostky`:
   ```
   $ cd www
   $ git clone https://github.com/edumach/kostky
   ``` 
4. Tím vznikne adresář `~/www/kostky/`
5. Zkontroluj jeho obsah:
   ```
   $ cd kostky
   $ ls -l
   ```
6. Zkontroluj funkčnost webu na URL `https://tux.panska.cz/~10XPrijmeniJ/kostky`

## Další postup

Po načtení stránky se:

* **náhodně vygenerují dvě čísla 1–6**,
* zobrazí se **čísla i obrázky kostek**,
* vypočítá se **součet bodů**,
* tlačítko **„Házet znovu“** načte stránku znovu (nový hod).


### (1) Kde se v HTML píše PHP

PHP kód se zapisuje mezi značky:

```php
<?php
  // PHP kód
?>
```

PHP se **vykoná na serveru** a do HTML se vloží výsledek.

Do souboru `index.php` můžeme PHP psát **kdekoliv**, ale nejčastěji:

* na **začátku souboru** (logika),
* nebo **uvnitř HTML** (výpis hodnot).


### (2) Vygenerování náhodných hodů kostkami

Na **začátek souboru `index.php`** (úplně nahoru) přidej:

```php
<?php
  $c1 = rand(1, 6);
  $c2 = rand(1, 6);
?>
```

**Vysvětlení:**


* `rand(1, 6)` → náhodné číslo od 1 do 6
* `$c1`, `$c2` → proměnné
* `$` **patří k názvu proměnné**



### (3) Vypsání hozených čísel do stránky

Najdi v HTML tuto část:

```php
<p>
  Na 1. kostce padlo číslo
  <br>
  Na 2. kostce padlo číslo
</p>
```

A **doplň PHP výpisy**:

```php
<p>
  Na 1. kostce padlo číslo <?php echo $c1; ?>
  <br>
  Na 2. kostce padlo číslo <?php echo $c2; ?>
</p>
```

**Vysvětlení:**

* `echo` → vypíše hodnotu do HTML
* PHP se **přepíná do HTML a zpět**
* prohlížeč už **PHP neuvidí**, jen výsledek



### (4) Zobrazení obrázků kostek

Obrázky jsou ve složce:

```
~/www/kostky/img/
```

a mají názvy:

```
k_1.gif, k_2.gif ... k_6.gif
```

Pod předchozí odstavec přidej:

```php
<p>
  <?php
    echo "<img src='img/k_$c1.gif'>";
    echo "<img src='img/k_$c2.gif'>";
  ?>
</p>
```

**Vysvětlení:**

* v proměnné `$c1` je uložené pouze číslo
* vznikne např. `<img src='img/k_4.gif'>`


### (5) Výpočet součtu

Do PHP části nahoře doplň:

```php
<?php
  $c1 = rand(1, 6);
  $c2 = rand(1, 6);
  $soucet = $c1 + $c2;
?>
```

### (6) Výpis součtu do stránky

Najdi:

```html
<p>
  Součet bodů je 
</p>
```

Uprav na:

```php
<p>
  Součet bodů je
  <strong><?php echo $soucet; ?></strong>
</p>
```


### Shrnutí

- PHP:
  - **vygeneruje čísla**
  - **spočítá součet**
  - PHP **nefunguje bez serveru**, v prohlížeči **nikdy neuvidíš PHP kód**.
- HTML:
  - **zobrazí text**
  - **zobrazí obrázky**
- Tlačítko znovu načte stránku -> **nový hod**

---

## Rozšíření 1 (DOUBLE)

Pokud **padnou stejná čísla** (např. 3 a 3),
* pod součtem se zobrazí text **DOUBLE**,
* text bude **červený** (pomocí CSS).


### (A) Podmíněné zobrazení textu DOUBLE

Pod odstavec se součtem přidej:

```php
<?php
if ($c1 == $c2) {
    echo '<p class="double">DOUBLE</p>';
}
?>
```

**Vysvětlení:**

* PHP rozhoduje, **zda se HTML vůbec vygeneruje**
* pokud double **není**, text v HTML **neexistuje**


### (B) Přidání CSS stylu

Do části `<head>` přidej jednoduchý styl:

```html
<style>
.double {
  color: red;
  font-weight: bold;
}
</style>
```


### Shrnutí

1. PHP:
   - vygeneruje hody
   - spočítá součet
   - porovná čísla
2. HTML:
   - zobrazí text a obrázky
3. CSS:
   - určí, jak má DOUBLE vypadat

---

## Rozšíření 2 (VELKÝ HOD)

- Pokud je součet 10 a víc, vypíše se zeleně text "VELKÝ HOD".
- Technicky jde o přidání vhodné podmínky a CSS stylu.

## Odevzdání

Funkční aplikace na URL `https://tux.panska.cz/~10XPrijmeniJ/kostky` včetně **obou** rozšíření.   
