- [Složitost algoritmů](#složitost-algoritmů)
  - [Čas a prostor výpočtu pro konkrétní vstup](#čas-a-prostor-výpočtu-pro-konkrétní-vstup)
  - [Časová a prostorová složitost algoritmu](#časová-a-prostorová-složitost-algoritmu)
  - [Složitost v nejlepším, nejhorším a průměrném případě](#složitost-v-nejlepším-nejhorším-a-průměrném-případě)
  - [Asymptotická notace](#asymptotická-notace)
- [Třídy složitosti](#třídy-složitosti)
  - [Třídy P a NP](#třídy-p-a-np)
  - [Převoditelnost problémů](#převoditelnost-problémů)
  - [NP těžkost a NP úplnost](#np-těžkost-a-np-úplnost)
  - [Příklady NP úplných problému a převodů mezi nimi](#příklady-np-úplných-problému-a-převodů-mezi-nimi)
- [Metoda rozděl a panuj](#metoda-rozděl-a-panuj)
  - [Princip rekurzivního dělení prolému na podproblémy](#princip-rekurzivního-dělení-prolému-na-podproblémy)
  - [Výpočet složitosti pomocí rekurentních rovnic](#výpočet-složitosti-pomocí-rekurentních-rovnic)
  - [Kuchařková věta](#kuchařková-věta)
  - [Aplikace (Mergesort, násobení dlouhých čísel, Strassenův algoritmus)](#aplikace-mergesort-násobení-dlouhých-čísel-strassenův-algoritmus)
- [Dynamické programování](#dynamické-programování)
- [Binární vyhledávací stromy](#binární-vyhledávací-stromy)
  - [Definice vyhledávacího stromu](#definice-vyhledávacího-stromu)
  - [Operace s nevyvažovanými stromy](#operace-s-nevyvažovanými-stromy)
  - [AVL stromy](#avl-stromy)
- [Haldy](#haldy)
  - [Binárnní halda](#binárnní-halda)
- [Hešování](#hešování)
  - [Hešování s přihrádkami](#hešování-s-přihrádkami)
  - [Otevřená adresace](#otevřená-adresace)
- [Třídění](#třídění)
  - [Primitivní třídící algoritmy](#primitivní-třídící-algoritmy)
  - [Třídění haldou](#třídění-haldou)
  - [Quicksort](#quicksort)
  - [Dolní odhad složitosti porovnávacích třídících algoritmů](#dolní-odhad-složitosti-porovnávacích-třídících-algoritmů)
  - [Přihrádkové třídění čísel a řetězců](#přihrádkové-třídění-čísel-a-řetězců)
- [Grafové algoritmy](#grafové-algoritmy)
  - [Prohledávání do šířky a do hloubky](#prohledávání-do-šířky-a-do-hloubky)
  - [Detekce komponent souvislosti](#detekce-komponent-souvislosti)
  - [Topologické třídění orientovaných grafů](#topologické-třídění-orientovaných-grafů)
  - [Nejkratší cesty v ohodnocených grafech](#nejkratší-cesty-v-ohodnocených-grafech)
  - [Minimální kostra grafu](#minimální-kostra-grafu)
  - [Toky v sítích](#toky-v-sítích)
- [Algoritmy vyhledávání v textu](#algoritmy-vyhledávání-v-textu)
- [Algebraické algoritmy](#algebraické-algoritmy)

# Složitost algoritmů

Obecně: měření je nezávislé na konkrétním zařízení. Pracujeme s teoretickým modelem (Von neumannovský počítač), který se skládá z:

- řídicí jednotka – koordinuje činnost ostatních jednotek
- aritmeticko-logická jednotka (ALU) – provádí numerické výpočty, ...
- operační paměť – uchovává data
- vstupní zařízení – vstup pro data
- výstupní zařízení – zápis výsledků

Spustíme-li program na reálném počítači několikrát, nejspíš naměříme o něco rozdílné časy, my ale chceme prostředek na měření doby běhu obecně popsaného algoritmu.

## Čas a prostor výpočtu pro konkrétní vstup

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=42))

Zavedeme _elementární operaci_ (to, co normální procesor
zvládne jednou nebo nejvýše několika instrukcemi, př. sčítání, násobení). _Elementární operace_ se vykoná za jednotkový čas (zbavili jsme se jednotky).

```
Vstup: Číslo n

1. Pro i = 1, ... , n opakuj:
2.      Pro j = 1, ... , i opakuj:
3.          Vytiskni *
```

Pro $i = 1$ se provede vnitřní cyklus jedenkrát, pro $i = 2$ dvakrát, pro $i = n$ se provede $n$-krát. Dohromady se vytiskne $1 + 2 + 3 + ... + n = n(n + 1)/2= 2n^2 + 2n$ hvězdiček.

Časová složitost pro konkrétní je tedy matematická funkce, která popisuje, jak se algoritmus chová pro různá $n$ (hodnota na vstupu). Odpadá tak nutnost program spouštět.

Konstanty můžeme rovněž zanedbat, jsou strojově závislé (elementární operace se reálně liší v rychlostech) a chování algoritmu pro velká $n$ nijak zásadně neovlivňují. Dále ve výrazu $2n^2 + 2n$ je pro velká $n$ člen $2n^2$ obrovský oproti $2n$, takže $2n$ můžeme klidně vynechat.

## Časová a prostorová složitost algoritmu

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=46))

Umíme dobu běhu vyjádřit jako funkci vstupu. Vstup ale bývá složitější než jedno číslo. Zavedeme _míru velikosti vstupu_ a čas budeme vyjadřovat v závislosti na ní. Pokud program pro různé vstupy téže velikosti běží různě dlouho, uvážíme ten nejpomalejší případ. Tím dostaneme funkci, které se říká _časová složitost_ algoritmu.

Velikost vstupu se určuje různě. Pokud je vstupem posloupnost čísel, obvykle za velikost považujeme jejich počet. Podobně za velikost řetězce znaků prohlásíme počet znaků. Pro Euklidův algoritmus vezmeme za velikost vstupu maximum ze zadaných čísel.

Kuchařka pro určení velikosti vstupu (není to řádná matematická definice):

1. Ujasníme si, jak se měří velikost vstupu.
2. Určíme maximální možný počet $f(n)$ elementárních operací algoritmu provedených
   na vstupu o velikosti $n$ (popř. najdeme alespoň horní odhad).
3. V $f(n)$ necháme pouze nejrychleji rostoucí člen ($n^2+n$ → $n^2$)
4. Seškrtáme multiplikativní konstanty

Pro určení prostorové (paměťové) složitosti analogicky spočítáme kolik nejvíce _elementární paměťových buněk_ bude v každém okamžiku použito. Množství spotřebovaných paměťových buněk v závislosit na velikosti vstupu $n$ vyjádříme pomocí funkce $f(n)$ (popř. uděláme horní odhad), aplikujeme čtyřbodovou kuchařku a výsledek zapíšeme pomocí notace $O(g(n))$

## Složitost v nejlepším, nejhorším a průměrném případě

## Asymptotická notace

f(n) je třídy O(g(n)),
jestliže existuje taková kladná reálná konstanta c, že pro skoro všechna n platí f(n) ≤
cg(n). Skoro všemi n se myslí, že nerovnost může selhat pro konečně mnoho výjimek, tedy
že existuje nějaké přirozené n0 takové, že nerovnost platí pro všechna $n ≥ n_{0}$. Funkci g(n)
se pak říká asymptotický horní odhad funkce f(n).

# Třídy složitosti

## Třídy P a NP

## Převoditelnost problémů

## NP těžkost a NP úplnost

## Příklady NP úplných problému a převodů mezi nimi

# Metoda rozděl a panuj

## Princip rekurzivního dělení prolému na podproblémy

## Výpočet složitosti pomocí rekurentních rovnic

## Kuchařková věta

## Aplikace (Mergesort, násobení dlouhých čísel, Strassenův algoritmus)

# Dynamické programování

# Binární vyhledávací stromy

## Definice vyhledávacího stromu

## Operace s nevyvažovanými stromy

## AVL stromy

# Haldy

## Binárnní halda

# Hešování

## Hešování s přihrádkami

## Otevřená adresace

# Třídění

## Primitivní třídící algoritmy

## Třídění haldou

## Quicksort

## Dolní odhad složitosti porovnávacích třídících algoritmů

## Přihrádkové třídění čísel a řetězců

# Grafové algoritmy

## Prohledávání do šířky a do hloubky

## Detekce komponent souvislosti

## Topologické třídění orientovaných grafů

## Nejkratší cesty v ohodnocených grafech

## Minimální kostra grafu

## Toky v sítích

# Algoritmy vyhledávání v textu

# Algebraické algoritmy
