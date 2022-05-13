---
title: Algoritmy
tags: [Notebooks/IVT]
created: 2022-05-12T16:51:02.192Z
modified: 2022-05-13T09:12:22.387Z
---

# Algoritmy

- [Algoritmy](#algoritmy)
  * [Třídící algoritmy](#třídící-algoritmy)
    + [Bublinkové třídění](#bublinkové-třídění)
    + [Třídění podle minima (Selection sort)](#třídění-podle-minima-selection-sort)
    + [Třídění zatřiďováním (Insertion sort)](#třídění-zatřiďováním-insertion-sort)
    + [Přihrádkové třídění (Counting sort)](#přihrádkové-třídění-counting-sort)
  * [Hledání kořenů funkce](#hledání-kořenů-funkce)
    + [Iterace](#iterace)
    + [Půlení intervalu](#půlení-intervalu)
    + [Metoda sečen](#metoda-sečen)
  * [Hledání prvku v poli](#hledání-prvku-v-poli)
    + [Hledání v neuspořádaném poli](#hledání-v-neuspořádaném-poli)
    + [Hledání v uspořádaném poli](#hledání-v-uspořádaném-poli)
      - [pokud se prvky mohou opakovat:](#pokud-se-prvky-mohou-opakovat)
  * [Eukleidův algoritmus](#eukleidův-algoritmus)
  * [Převody číselných soustav](#převody-číselných-soustav)
    + [Z desítkové na _n_](#z-desítkové-na-n)
    + [Z _n_ na desítkovou](#z-n-na-desítkovou)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## Třídící algoritmy
### Bublinkové třídění
```pascal
program trideni;
const n = 10;
  var P: array[1..n] of byte;
    i, j, pom : byte;
begin
  Randomize;
 for i := 1 to n do P[i] := Random(50);
 for i := 1 to n do write(P[i]:4);
 writeln;
 for i := 2 to n do
       for j := n downto i do
       if P[j-1] > P[j] then begin {pokud jsou prvky opačně, vyměň je}
            pom := P[j];
            P[j]:= P[j-1];
            P[j-1] := pom;
       end;
   for i := 1 to n do write(P[i]:4); readln;
 end.
```

### Třídění podle minima (Selection sort)
```pascal
program trideni;
const n = 10;
  var P: array[1..n] of byte;
    i, j, min, pom : byte;		{v proměnné min bude index minimálního prvku}
begin
  Randomize;
  for i := 1 to n do P[i] := Random(50);
  for i := 1 to n do write(P[i]:4);
  writeln;
  for i := 1 to (n-1) do		{nesetříděný úsek začíná i-tým prvkem}
    begin
      min := i;				{první prvek úseku je prozatímní minimum}
      for j := i + 1 to n do		{v cyklu hledám, je-li vpravo menší prvek}
        if P[j] < P[min] then min := j;	{pokud je, jeho index uložím do min}
      pom := P[i];			{vyměním první prvek úseku s minimálním}
      P[i] := P[min];
      P[min] := pom;
    end;				{v dalším kroku hledám opět od následující pozice}
   for i := 1 to n do write(P[i]:4);
  readln;
end.
```

### Třídění zatřiďováním (Insertion sort)
```pascal
program trideni;
const n = 10;
  var P: array[1..n] of byte;
    i, j, X : byte;
    mensi : boolean;
begin
  Randomize;
  for i := 1 to n do P[i] := Random(50);
  for i := 1 to n do write(P[i]:4);  writeln;
  for i := 2 to n do			{zatřiďuji číslo z pozice i}
    begin
       X := P[i];			{hodnotu uložím do pomocné proměnné	X}
       j := i-1;				{vlevo od pozice i hledám umístění hodnoty}
       mensi := X < P[j];
       while mensi do		{dokud je X menší než prvky vlevo, postupuji vlevo}
             begin
             P[j+1]:= P[j];	{větší prvky posouvám o jednu pozici vpravo}
             dec(j);    //j := j-1
             if j = 0 then mensi := false
             else mensi := X < P[j];
             end;
       P[j+1] := X;	{pokud dojdu na začátek, nebo levý prvek je menší, umístím X}
    end;
   for i := 1 to n do write(P[i]:4); readln;
 end.
```

### Přihrádkové třídění (Counting sort)
```pascal
program prihradky;
const M = 50;
      maxc = 10;
var A : array[1..M] of byte;
    P : array[1..maxc] of byte;
    n, i, j, k : byte;
begin
  Randomize;
  write('Zadej pocet cisel do 50: ');
  readln(n);
  for i :=  1 to n do A[i] := Random(maxc)+1;
  for i := 1 to n do write(A[i]:3);
  writeln; writeln;
  for i := 1 to maxc do P[i]:= 0;
  for i := 1 to n do inc(P[A[i]]); 		{zaznamenávám, kolikrát je tam dané číslo}
  k := 0;						{k index pro přepsání pole A}
  for i := 1 to maxc do
       for j := 1 to P[i] do
             begin inc(k);
             A[k]:=i;				{zapisuji hodnotu do pole A}
             end;
  for i := 1 to n do write(A[i]:3);
  readln;
end.
```

## Hledání kořenů funkce
### Iterace
```pascal
procedure iterace(a,b:real; h:Fce); {a,b – meze intervalu, kde hledám kořeny,
 						h – fce, pro kterou hledám kořeny}
var x:real;
    koren:boolean;			{indikuje nalezení kořene}
begin
   koren := false;
     x:=a;
     while x<=b do		{dokud je x menší nebo rovno b opakuj}
           begin
                if abs(h(x))<eps then	{liší-li se h(x) od nuly o méně než eps}
                begin
                writeln('Koren je: ',x:4:2);  {x je kořen}
                koren:= true;			     {kořen nalezen}	
                end;
                x:= x+delta;			   {zvětši x o konstantu delta}  
           end;
     if not koren then writeln('koren v danem intervalu neexistuje');
 end;
```

### Půlení intervalu
```pascal
procedure puleni(a,b:real;h:Fce);
var x:real;
begin
    repeat x:=(a+b)/2;		{střed intervalu}
     if  h(x)*h(a)>0 then a:= x   {podle znamének fčních hodnot určím nový interval}
                     else b :=x;
     until abs(h(x))<eps;		{končím, pokud je hodnota „skoro“ nula}
     writeln('Koren je: ',x:4:2);
end;
```

### Metoda sečen
```pascal
procedure secny(a,b:real;h:Fce);
var x:real;
begin
  repeat
    x := b+ h(b)*(a-b)/(h(b)-h(a));  {výpočet průsečíku}
        if  h(x)*h(a)>0 then a:= x	 {porovnání znamének, určení nového intervalu}
                     else b :=x;
  until abs(h(x))<eps;
  writeln('koren secnami je: ',x:4:2);
 end;
```

## Hledání prvku v poli
### Hledání v neuspořádaném poli
```pascal
program hledani;
const M =50;
var P : array[1..M] of byte;		//deklarace pole
  i, n,cislo : byte;
  nalezeno : boolean = false;		//proměnná pro uložení, zda bylo číslo nalezeno

begin
 write('Zadej pocet cisel v poli - do 50: ');
 readln(n);
 Randomize;
 for i := 1 to n do P[i] := Random(21)+10;	//generování pole
 for i := 1 to n do write(P[i]:4);			//výpis pole
 writeln;
 write('Zadej cislo k hledani: ');
 readln(cislo);

//1. řešení – najde první výskyt hledaného čísla
 i := 1;
 while (i <= n) and (P[i]<>cislo) do		//procházení pole, dokud nenarazím na 
       inc(i);						//hledané číslo nebo konec pole
 if i > n then writeln('Nenalezeno')
    else writeln('Nalezeno na ',i,'. pozici');
 writeln;

//2. řešení – vypíše všechny pozice hledaného čísla
 for i := 1 to n do
     if cislo = P[i] then			//porovnává prvky pole s hledanou hodnotou
              begin
                write(i:4);			//vypíše pozici hledaného čísla
                nalezeno := true;
              end;
 writeln;
  if nalezeno then
  writeln('Vypsana cisla jsou jeho pozice')
  else writeln('cislo nebylo nalezeno');
 readln;
end.                                       
```

### Hledání v uspořádaném poli
```pascal
program hledej;
const n=20;
var A:array[1..n] of integer;
 i, j, horni, dolni:byte;
 	cislo:integer;
begin
 Randomize;
 A[1] := Random(5);   //první prvek generuji zvlast
  for i := 2 to n do A[i]:= A[i-1] + random(10);  //nagenerovani pole cisel
 for i := 1 to N do write(A[i]:4) ;			 //vypsani pole
 writeln;
 write('zadej cislo: ');
 readln(cislo);			//nacteni hledane hodnoty
 dolni := 1;
 horni := N;
 repeat j := (dolni + horni) div 2;		//výpočet indexu prostředního prvku
  if cislo < A[j] then horni := j-1    //prostredni prvek porovnam s hledanym
     else dolni := j+1;			//posun mezi pro hledani
 until (cislo = A[j]) or (dolni > horni);
{-----------------------------------------}
 if A[j] = cislo then writeln('cislo ',cislo,' je na pozici ',j)
    else writeln('cislo se nevyskytuje');
 readln;
 end.
```
#### pokud se prvky mohou opakovat:
```pascal
{-----------------------------------------}
if A[j] = cislo then
   begin
     repeat
       dec(j)
     until A[j] <> cislo;
     dolni := j+1;
     repeat
       inc(j)
     until A[j] <> cislo;
     horni := j-1;
     writeln(cislo,' je na pozicich od ',dolni,' po ',horni)
   end
   else writeln(cislo,' se nevyskytuje');     
readln;
end.
```

## Eukleidův algoritmus
```pascal
program eukleid;
var a,b:integer;
BEGIN
write('zadej dve cisla: ');
readln(a,b);
while a <> b do				{algorimtus založený na odčítání}
 		if a > b then a := a - b
    		else b := b - a;
writeln('Delitel je : ',a);

write('zadej dve cisla: ');
readln(a,b);
while (a <> 0) and (b <> 0) do	{využití funkce mod}
 	if a > b then a := a mod b
        else b := b mod a ;
 	{if b = 0 then writeln('delitel pres mod je: ', a)
        else writeln('delitel pres mod je: ', b);}
	writeln('delitel pres mod je: ',a+b);
readln
END.
```

## Převody číselných soustav
### Z desítkové na _n_
- celočíselně dělíme základem a zapisujeme zbytky, které pak "odzadu" vypíšeme
### Z _n_ na desítkovou
- převedeme si číslo na řetězec a použijeme for-in cyklus
```pascal
//uses math, sysutils
e := length(string)-1;
vysl := 0;
for char in string do begin
  vysl := vysl + strtoint(char)*round(power(zaklad, e));
end;
```
