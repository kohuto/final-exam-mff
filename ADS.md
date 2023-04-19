- [Složitost algoritmů](#slozitost-algoritmu)
  - [Čas a prostor výpočtu pro konkrétní vstup](#cas-a-prostor-vypoctu-pro-konkretni-vstup)
  - [Časová a prostorová složitost algoritmu](#casova-a-prostorova-slozitost-algoritmu)
  - [Složitost v nejlepším, nejhorším a průměrném případě](#slozitost-v-nejlepsim-nejhorsim-a-prumernem-pripade)
  - [Asymptotická notace](#asymptoticka-notace)
- [Třídy složitosti](#tridy-slozitosti)
  - [Třídy P a NP](#tridy-p-a-np)
  - [Převoditelnost problémů](#prevoditelnost-problemu)
  - [NP těžkost a NP úplnost](#np-tezkost-a-np-uplnost)
  - [Příklady NP úplných problému a převodů mezi nimi](#priklady-np-uplnych-problemu-a-prevodu-mezi-nimi)
- [Metoda rozděl a panuj](#metoda-rozdel-a-panuj)
  - [Princip rekurzivního dělení problému na podproblémy](#princip-rekurzivniho-deleni-problemu-na-podproblemy)
  - [Výpočet složitosti pomocí rekurentních rovnic](#vypocet-slozitosti-pomoci-rekurentnich-rovnic)
  - [Kuchařková věta](#kucharkova-veta)
  - [Aplikace (Mergesort, násobení dlouhých čísel, Strassenův algoritmus)](#aplikace-mergesort-nasobeni-dlouhych-cisel-strassenuv-algoritmus)
- [Dynamické programování](#dynamicke-programovani)
- [Binární vyhledávací stromy](#binarni-vyhledavaci-stromy)
  - [Definice vyhledávacího stromu](#definice-vyhledavaciho-stromu)
  - [Operace s nevyvažovanými stromy](#operace-s-nevyvazovanymi-stromy)
    - [Hledání vrcholu s klíčem $x$](#hledani-vrcholu-s-klicem-x)
    - [Minimum](#minimum)
    - [Vkládání](#vkladani)
    - [Mazání vrcholu $v$](#mazani-vrcholu-v)
  - [AVL stromy](#avl-stromy)
- [Haldy](#haldy)
  - [Binární halda](#binarni-halda)
    - [Nalezení prvku s nejmenším klíčem](#nalezeni-prvku-s-nejmensim-klicem)
    - [Přidání nového prvku](#pridani-noveho-prvku)
    - [Odebrání prvku s nejmenším klíčem](#odebrani-prvku-s-nejmensim-klicem)
    - [Konstrukce haldy](#konstrukce-haldy)
- [Hešování](#hesovani)
  - [Hešování s přihrádkami](#hesovani-s-prihradkami)
  - [Otevřená adresace](#otevrena-adresace)
- [Třídění](#trideni)
  - [Primitivní třídící algoritmy](#primitivni-tridici-algoritmy)
    - [Bubblesort](#bubblesort)
    - [Insertsort](#insertsort)
    - [Selectsort](#selectsort)
  - [Třídění haldou](#trideni-haldou)
  - [Quicksort](#quicksort)
  - [Dolní odhad složitosti porovnávacích třídících algoritmů](#dolni-odhad-slozitosti-porovnavacich-tridicich-algoritmu)
  - [Přihrádkové třídění čísel a řetězců](#prihradkove-trideni-cisel-a-retezcu)
- [Grafové algoritmy](#grafove-algoritmy)
  - [Prohledávání do šířky a do hloubky](#prohledavani-do-sirky-a-do-hloubky)
  - [Detekce komponent souvislosti](#detekce-komponent-souvislosti)
  - [Topologické třídění orientovaných grafů](#topologicke-trideni-orientovanych-grafu)
  - [Nejkratší cesty v ohodnocených grafech](#nejkratsi-cesty-v-ohodnocenych-grafech)
  - [Minimální kostra grafu](#minimalni-kostra-grafu)
  - [Toky v sítích](#toky-v-sitich)
- [Algoritmy vyhledávání v textu](#algoritmy-vyhledavani-v-textu)
- [Algebraické algoritmy](#algebraicke-algoritmy)

# Složitost algoritmů

([průvodce](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=6))

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

```python
def triangle(n):
  for i in range(1, n+1):
    for j in range(1, i+1):
      print("*", end="")
    print()
```

Pro $i = 1$ se provede vnitřní cyklus jedenkrát, pro $i = 2$ dvakrát, pro $i = n$ se provede $n$-krát. Dohromady se vytiskne $1 + 2 + 3 + \dots + n = n(n + 1)/2= 2n^2 + 2n$ hvězdiček.

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

Funkci $g(n)$, která zbude, nazveme asymptotickou časovou složitostí algoritmu a tento fakt
označíme výrokem „algoritmus má časovou složitost $O(g(n))$“.

Pro určení prostorové (paměťové) složitosti analogicky spočítáme kolik nejvíce _elementární paměťových buněk_ bude v každém okamžiku použito. Množství spotřebovaných paměťových buněk v závislosit na velikosti vstupu $n$ vyjádříme pomocí funkce $f(n)$ (popř. uděláme horní odhad), aplikujeme čtyřbodovou kuchařku a výsledek zapíšeme pomocí notace $O(g(n))$

## Složitost v nejlepším, nejhorším a průměrném případě

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=49))

Složitost v nejhorším případě viz výše.

Funkci popisující _Složitost v průměrném případě_ je definovaná jako aritmetický průměr časových (prostorových) nároků algoritmu přes všechny vstupy dané velikosti.

## Asymptotická notace

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=50))

$f(n)$ je třídy $O(g(n))$, jestliže existuje $\exists n_{0}$ tž. $\forall n \geq n_{0}$ $\exists$ kladná reálná konstanta c, pro kterou platí $f(n) \leq cg(n)$. Tzn. nerovnost platí pro všechna $n$ až na konečně mnoho výjimek. Funkci $g(n)$ nazveme asymptotický horní odhad funkce $f(n)$.

Poněkud formálněji bychom se na zápis $O(g)$ mohli dívat jako na množinu všech funkcí $f$, které splňují uvedenou definici.

S opačnou nerovností zavedeme dolní odhad. Značíme $f(n)$ je třídy $\Omega(g(n))$.

Řekneme, že funkce $f(n)$ je třídy $\Theta(g(n))$, jestliže $f(n)$ je jak třídy $O(g(n))$, tak třídy $\Omega(g(n))$.

# Třídy složitosti

## Třídy P a NP

## Převoditelnost problémů

## NP těžkost a NP úplnost

## Příklady NP úplných problému a převodů mezi nimi

# Metoda rozděl a panuj

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=243))
([kuchařka](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=57))

Naším cílem bude rozkládat zadaný problém na menší podproblémy a z jejich výsledků pak skládat řešení celého problému. S jednotlivými podproblémy potom naložíme stejně – opět je
rozložíme na ještě menší a tak budeme pokračovat, než se dostaneme k tak jednoduchým vstupům, že je už umíme vyřešit přímo.

## Princip rekurzivního dělení problému na podproblémy

## Výpočet složitosti pomocí rekurentních rovnic

## Kuchařková věta

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=253))

Věta (kuchařka na řešení rekurencí): Rekurentní rovnice $T(n) = a \cdot T(n/b) + \Theta(n^c)$,
$T(1) = 1$ má pro konstanty $a \geq 1$, $b > 1$, $c \geq 0$ řešení:

- $T(n) = \Theta(n^c \log n)$, pokud $a/b^c = 1$
- $T(n) = \Theta(n^c)$, pokud $a/b^c < 1$
- $T(n) = \Theta(n^{\log_{b} a})$, pokud $a/b^c > 1$

## Aplikace (Mergesort, násobení dlouhých čísel, Strassenův algoritmus)

# Dynamické programování

Dynamické programování je technika, kterou jde z pomalého rekurzivního algoritmu vyrobit pěkný polynomiální (až na výjimečné případy).

# Binární vyhledávací stromy

Strom nazveme binární, pokud je zakořeněný a každý vrchol má nejvýše dva
syny, u nichž rozlišujeme, který je levý a který pravý. Vrcholy rozdělíme podle vzdálenosti od kořene do hladin: v nulté hladině leží kořen, v první jeho synové atd. Pro vrchol $v$ binárního stromu $T$ značíme:

- $T(v)$ – podstrom obsahující vrchol $v$ a všechny jeho potomky
- $l(v)$ a $r(v)$ – levý a pravý syn vrcholu $v$
- $L(v)$ a $R(v)$ – levý a pravý podstrom vrcholu $v, tedy $T(l(v))$ a $T(r(v))$
- h(v) – hloubka stromu $T(v)$, čili maximum z délek cest z $v$ do listů

## Definice vyhledávacího stromu

([kuchařka](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=75))
([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=185))

Binární vyhledávací strom (BVS) je binární strom, jehož každému vrcholu $v$
přiřadíme unikátní klíč $k(v)$ z univerza. Přitom musí pro každý vrchol $v$ platit:

- Kdykoliv $a \isin L(v)$, pak $k(a) < k(v)$.
- Kdykoliv $b \isin R(v)$, pak $k(b) > k(v)$.

Jinak řečeno, vrchol v odděluje klíče v levém a pravém podstromu.

## Operace s nevyvažovanými stromy

### Hledání vrcholu s klíčem $x$

Procházíme stromem od kořene a každý vrchol $v$ porovnáme s $x$. Pokud je $x < k(v)$, pak je $x$ v levém podstromu a naopak. Nejpozději v listu najdeme $x$.

### Minimum

Jdeme doleva dokud to jde. Když nejde jít doleva, tak jsme našli minimum.

### Vkládání

Funguje stejně jako hledání - v momentě, kdy by vyhledávací algoritmus měl přejít do neexistujícího vrcholu, připojíme tam nový list.

### Mazání vrcholu $v$

1. je-li $v$ list, smažeme ho
2. má-li $v$ právě jednoho syna, nahradíme $v$ tímto synem (vytřihneme $v$)
3. má-li $v$ dva syny, nalezneme následníka $s$ vrcholu $v$, tedy nejlevější vrchol v pravém podstromu. $s$ smažeme ($s$ má max jednoho syna) a hodnotu v $s$ přesuneme do $v$

Postupně smažeme 2, 4 a 3:
![Alt text](images\delete_in_bst.png)

## AVL stromy

Binární vyhledávací strom nazveme hloubkově vyvážený, pokud pro každý jeho
vrchol v platí $$h(l(v)) − h(r(v)) \leq 1$$ Jinými slovy, hloubka levého a pravého podstromu se vždy liší nejvýše o jedna. AVL strom na n vrcholech má hloubku $\Theta(\log n)$

# Haldy

## Binární halda

([kuchařka](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=27))
([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=253#page=84))

_\*Klíč přiřazený prvku $x$ budeme značit $k(x)$. Kdykoliv budeme mluvit o porovnávání prvků, myslíme tím podle klíčů._

Halda je datová struktura tvaru binárního stromu, v jehož každém vrcholu je uložen jeden prvek. Přitom platí:

1. Tvar haldy: Všechny hladiny kromě poslední jsou plně obsazené. Poslední hladina je zaplněna zleva.
2. Haldové uspořádání: Je-li $v$ vrchol a $s$ jeho syn, platí $k(v) \leq k(s)$.

Halda s $n$ prvky má $\lfloor \log_2 n \rfloor + 1$ hladin.

Halda podporuje následující operace:

- přidání nového prvku
- nalezení prvku s nejmenším klíčem
- odebrání prvku s nejmenším klíčem

Haldu s $N$ prvky uložíme do pole. Prvek na pozici $k$ má levého syna na pozici $2k$ a pravého na pozici $2k + 1$ (pokud existují). Otec vrcholu $k$ leží na pozici $\lfloor k/2 \rfloor$

### Nalezení prvku s nejmenším klíčem

Vydáme-li se z kořene dolů po libovolné cestě, klíče nemohou klesat. Proto
se v kořeni stromu musí nacházet jeden z minimálních prvků.

### Přidání nového prvku

Podmínka na tvar haldy nám dovoluje přidat nový list na konec poslední hladiny. Pokud by tato hladina byla plná, můžeme založit novou s jediným listem úplně vlevo. Tím dostaneme strom správného tvaru. Nemusí již ovšem platit, že nový list $l$ je větší než jeho otec $o$ (podmínka $k(l) > k(o)$). V takovém případě list s otcem prohodíme, což může způsobit chybu o hladinu výše, proto prohazujeme dále (potenciálně až do kořene). Prohození s otcem nemůže pokazit vztah s druhým synem, protože klíč v otci se zmenší.

### Odebrání prvku s nejmenším klíčem

Odstraníme nejpravější vrchol na nejnižší hladině a přesuneme ho do kořene. Strom má správný tvar, ale mohlo se pokazit uspořádání (kořen může být větší než synové). V takovém případě kořen prohodíme s menším z obou synů. Vztahy mezi kořenem a jeho syny jsou opravené, o hladinu níže ale mohl vzniknout obdobný problém. Analogicky „zabubláváme“ potenciálně až do listu.

### Konstrukce haldy

Prvky rozmístíme do vrcholů binárního stromu v libovolném pořadí – pokud máme strom uložený v poli, nemuseli jsme pro to udělat vůbec nic, prostě jenom začneme pozice v poli chápat jako indexy ve stromu. Pak budeme opravovat uspořádání od nejnižší hladiny až k té nejvyšší, tedy v pořadí klesajících indexů. Kdykoliv zpracováváme nějaký vrchol, využijeme toho, že celý podstrom pod ním je už uspořádaný korektně, takže na opravu vztahů mezi novým vrcholem a jeho syny stačí provést bublání dolů.

# Hešování

([kuchařka](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=88))
([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=276))

## Hešování s přihrádkami

Mějme množinu hodnot $U$, konečnou množinu přihrádek $P ={0, \dots , m − 1}$ a hešovací funkci, což bude nějaká funkce $h : U → P$, která každému prvku z $U$ přidělí jednu přihrádku. Chceme-li uložit množinu prvků $X \subseteq U$, pak $\forall x \isin X$ umístíme do přihrádky $h(x)$. Budeme-li pak hledat nějaký prvek $u \isin U$, najdeme ho v přihrádce $h(u)$.

kdykoliv máme nějakou hešovací funkci, můžeme si pořídit pole $p$ přihrádek, v každé pak „řetízek“ – spojový seznam hodnot. Tato jednoduchá datová struktura je jednou z možných forem hešovací tabulky.

Jakou má hešovací tabulka časovou složitost? Hledání, vkládání i mazání sestává z výpočtu hešovací funkce a projití řetízku v příslušné přihrádce. Pokud bychom uvažovali „ideální
hešovací funkci“, kterou lze spočítat v konstantním čase a která zadanou $n$-prvkovou množinu rozprostře mezi $m$ přihrádek dokonale rovnoměrně, budou mít všechny řetízky $n/m$ prvků. Zvolíme-li navíc počet přihrádek $m \isin \Theta(n)$, vyjde konstantní délka řetízku,
a tím pádem i časová složitost operací.

Ideální hešovací funkce je jako jednorožec (pro matfyzáka: jako ideální plyn) - neexistuje. Ty, které se však používají jsou např.:

- Lineární kongruence: $x \mapsto ax \mod m$  
  Zde $m$ je typicky prvočíslo a $a$ je nějaká dostatečně velká konstanta nesoudělná s $m$ ($a$ se nastavuje blízko př. $0.618m$)

### Přehešování

## Otevřená adresace

Opět si pořídíme pole s m přihrádkami $A[0], \dots , A[m − 1]$, jenže tentokrát se do každé přihrádky vejde jen jeden prvek. Pokud bychom tam potřebovali uložit další, použijeme náhradní přihrádku, bude-li také plná, zkusíme další, atd. (To je princip vkládání). Řekněme, že hešovací funkce každému prvku $x \isin U$ přiřadí jeho vyhledávací posloupnost $h(x, 0), h(x, 1), \dots , h(x, m − 1)$ určující pořadí přihrádek, do kterých se budeme snažit $x$ vložit. Budeme předpokládat, že posloupnost obsahuje všechna čísla přihrádek v dokonale náhodném pořadí.

Při vyhledávání budeme procházet přihrádky $h(x, 0), h(x, 1)$ atd. Zastavíme se, jakmile narazíme buď na $x$, nebo na prázdnou přihrádku.

Nemůže pouze smazat prvek (vyhledávání jiného prvku by skončilo předčasně, protože narazí na přihrádku, která v okamžiku vkládání byla plná, ale nyní už není). Prvky pouze označíme za smazané a až jich bude mnoho (třeba $m/4$), celou strukturu přebudujeme. To nás stojí amortizovaně konstantní čas na smazaný prvek.

V praxi se jako vyhledávací posloupnost používá:

- Lineární přidávání: $h(x, i) = (f(x) + i) \mod m$,
  kde $f(x)$ je „obyčejná“ hešovací funkce. Využíváme tedy po sobě jdoucí přihrádky.
- Dvojité hešování: $h(x, i) = (f(x) + i \cdot g(x)) \mod m$,
  kde $f : U → {0, \dots , m − 1}$ a $g : U → {1, \dots , m − 1}$ jsou dvě různé hešovací funkce a $m$ je prvočíslo. Díky tomu je $g(x)$ vždy nesoudělné s $m$ a posloupnost navštíví každou přihrádku právě jednou.

# Třídění

([průvodce](http://pruvodce.ucw.cz/static/pruvodce.pdf#page=61))

Na vstupu dostane algoritmus:

1. posloupnost $n$ prvků $a_1, \dots , a_n$.
2. komparátor – funkce, která pro dva prvky $a_i$ a $a_j$ odpoví, je-li $a_i < a_j$ , $a_i > a_j$ nebo $a_i = a_j$

Algoritmus pouze přerovnává prvky (nemění je) do nějakého pořadí $b_1 \leq b_2 \leq \dots \leq b_n$. Předpokládáme, že jedno porovnání i přesunutí zabere konstantní čas.

_Stabilní třídicí algoritmus_ - pořadí stejných prvků je na výstupu zachováno. Tedy pokud je
$p_i = p_j$ pro $i < j$, pak se $p_i$ ve výstupu objeví před $p_j$ .

Algoritmus _třídí prvky na místě_, pokud prvky neopouštějí paměťové buňky,
v nichž byly zadány (až na konstantí množství pracovních buněk). Povolujeme i pomocnou pracovní paměť, tedy libovolné množství číselných proměnných (indexy prvků, apod.).

## Primitivní třídící algoritmy

Termín _řazení_ je správnější. Data totiž nerozdělujeme do nějakých tříd, nýbrž je uspořádáváme, tedy řadíme, dle určitého kritéria. Termín _třídění_ je ale zažitější.

Společné rysy primitivních třídících algoritmů:

- jsou krátké
- jsou jednoduché
- třídí na místě
- mají kvadratickou časovou složitostí $\Theta(n^2)$.

Proto jsou použitelné pouze pro malá data

### Bubblesort

Opakovaně procházíme celé pole, dokud dochází k prohazování prvků. Jeden průchod postupně porovná všechny dvojice sousedních prvků $P[i]$ a $P[i+ 1]$. Pokud dvojice není správně uspořádaná, prvky prohodíme. Menší prvky se nám tak posunou blíže k začátku pole, zatímco větší prvky „bublají“ na jeho konec.

```python
def bubbleSort(arr):
    n = len(arr)
    swapped = False
    for i in range(n-1):
        if arr[i] > arr[i + 1]:
            swapped = True
            arr[i], arr[i + 1] = arr[i + 1], arr[i]
    if not swapped:
        return
```

### Insertsort

Na začátku pole vytváříme správně utříděnou posloupnost, kterou postupně rozšiřujeme. Na začátku $i$-tého kroku má tato utříděná posloupnost délku $i − 1$. V $i$-tém kroku určíme pozici $i$-tého čísla v dosud utříděné posloupnosti a zařadíme ho do utříděné posloupnosti (zbytek utříděné posloupnosti se posune o jednu pozici doprava).

```python
def insertionSort(arr):
	for i in range(1, len(arr)):
		key = arr[i]
		j = i-1
		while j >=0 and key < arr[j] :
				arr[j+1] = arr[j] # posun prvků o doprava
				j -= 1
		arr[j+1] = key # zařazení prvku
```

### Selectsort

Pole rozdělíme na dvě části: V první budeme postupně stavět setříděnou posloupnost a v druhé nám budou zbývat dosud nesetříděné prvky. V každém kroku nalezneme nejmenší ze zbývajících prvků a přesuneme jej na začátek druhé (a tedy i na konec první) části. Následně zvětšíme setříděnou část o 1.

```python
def selectionSort(array, size):
    for ind in range(size):
        min_index = ind
        for j in range(ind + 1, size):
            if array[j] < array[min_index]:
                min_index = j
        array[ind], array[min_index] = array[min_index], array[ind]
```

## Třídění haldou

([kuchařka](https://ksp.mff.cuni.cz/kucharky/programatorske-kucharky.pdf#page=29))

Vytvoříme nejdříve haldu z $N$ prvků na vstupu, načež z ní budeme postupně
$N$-krát odebírat nejmenší prvek.

Třídíme na místě - pole při plnění haldy obsahuje na svém začátku haldu a na konci zbytek vstupního pole, přitom zbytek pole se bude postupně zmenšovat a uvolňovat tak místo haldě.Naopak v druhé polovině algoritmu budeme zmenšovat haldu a do volného prostoru ukládat setříděné prvky. Proto chceme prvky získávat v opačném pořadí → stavíme max haldu.

Haldu vytváříme zabubláváním prvků od konce. Díky tomu vytvoříme haldu v lineárním čase.

```python
def heapify(arr, n, i):
	largest = i
	l = 2 * i + 1
	r = 2 * i + 2

# See if left/right child of root exists and is greater than root
	if l < n and arr[i] < arr[l]:
		largest = l
	if r < n and arr[largest] < arr[r]:
		largest = r

# Change root, if needed
	if largest != i:
		(arr[i], arr[largest]) = (arr[largest], arr[i])

# Heapify the root.
		heapify(arr, n, largest)

def heapSort(arr):
	n = len(arr)
	for i in range(n // 2 - 1, -1, -1):
		heapify(arr, n, i)
	for i in range(n - 1, 0, -1): # extract all elements
		(arr[i], arr[0]) = (arr[0], arr[i]) # swap
		heapify(arr, i, 0)
```

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
