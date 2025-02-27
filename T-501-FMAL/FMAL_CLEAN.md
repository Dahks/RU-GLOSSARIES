

Abstract machine
- An abstraction of the concept of a physical computer
- Mengi af gagnaskipan og reikniritum sem gera kleift að keyra forrit í L
	- ML gerir kleift að keyra forrit skrifað í L
- A device which allows the execution of programs written in L
- Hugræn því hún sleppir mörgum smáatriðum sem eru til staðar í tölvum
- An abstract machine for the programming language L, ML, is any set of data structures and algorithms which can perform the sotoreage and exeuction of programs written in L
- Generically composed of
	- A store -> serves to store data and programs
	- An interpreter -> The component that executes the instructions contained in programs.
- Implementations
	- In hardware
		- using physical devices ti implement a machine language coinciding with L
		- Fast -> direct execution by hardware
		- Complicated for high level languages
		- Impossible (very costly) to modify afterwards
		- Used for low-level languages
	- Simulation in software
		- Implement data structures and algorithms required by ML using programs written in another language L' (which has already been implemented)
		- Very flexible
		- lower performance -> more work (statement run twice or more)
	- Emulation in firmware
		- Microcode
		- Higher execution speed than a simulation in software
		- Less flexible -> re-writing requires special hardware

![Screenshot 2024-04-24 at 11.29.40.png](../images/Screenshot%202024-04-24%20at%2011.29.40.png)

útfærsla á sýndarvél
- útfærsla í vélbúnaði
	- Vélbúnaður útfærir reiknirit og Gagnaskipan sem ML þarfnast
	- Keyrsla forrits fáránlega hröð
	- ókostir
		- high-level mál nánast ómöguleg (bara low-level notað í raun)
		- breytingar ómögulegar
- Hermun með hugbúnaði
	- Nota forrit skrifað í örðu máli L' til að útfæra þá gagnaskipan og þau reiknirit sem ML þarfnast
	- Sveigjanlegt -> hægt að breyta, auðvelt í útfærslu
	- ókostir -> óskilvirkni -> overhead
- Hermun með fastbúnaði
	- Hermun á gagnaskipan og reikniritum í microcode
	- Hermt eftir ML með því að nota forrit
	- Forrit eru microforrit ekki í high-level máli
		- geymd í read-only minni
		- hratt en flókið að breyta (vélbúnaður til að endurskrifa ronly)

Hrein túlkuð útfærsla
![Screenshot 2024-04-24 at 11.58.16.png](../images/Screenshot%202024-04-24%20at%2011.58.16.png)
HLUTSKILGREINT FALL
- kostir
	- Sveigjanlegt -> auðvelt að þróa aflúsara
	- auðveldara í útfærslu yfir höfuð
- Óskilvirkt -> framkvæma afkóðun á setningum á meðan á keyrslu stendur

hrein þýdd útfærsla
![Screenshot 2024-04-24 at 12.08.41.png](../images/Screenshot%202024-04-24%20at%2012.08.41.png)
- Eiginleikar - >L frummál, LO markmál (object language), þýðingarferli óháð keyrslu
- Kostur -> Skilvirkni -> Þarf ekki að eyða tíma í afkóðun í keyrslu
- ókostir -> keyrsluvilla felur villu, erfiðara að útfæra aflúsara

Raunveruleikinn
- túlka það sem er lengst frá máli host machine en þýða rest
- þýðing fyrir keyrsluhraða
- túlkun fyrir sveigjanleika

Interpretive compilers
- þýða forrit yfir á millimál sem er síðan túlkað
- Hjálpar flytjanleika

Bootstrapping
- minimal subset of target language
- write compiler for that subset, in language of said subset
- hand translate minimal subset source code into assembly and assemble
	- working compiler for the subset of language
- write new compiler in language of working compiler to accept more source features
- copmile new compiler -> new compiler with larger subset
- reapeat until realized full features of source langauge

Rangt að segja að mál sé þýtt eða túlkað
- Útfærsluatriði
- hægt að útfæra sérhvert forritunarmál með því að nota annað hvort þýðanda eða túlk

Hierarchies of abstract machines
- That describe and implement complex software systems

Programming language
- Algorithms must be appropriately formalised using the constructs provided by a programming language
- Formally defined in terms of specific syntax and a precise semantic
- Implementing a programming language L means implementing an abstract machine which has L as its machine language
- Gervimál notuð til að tjá reiknirit
- Málskipan (syntax) L gerir okkur kleift að nota tiltekið mengi af skipunum til að skrifa forrit

Program
- A finite set of instructions of a language L -> data to interpreters

Syntax vs semantic
- syntax -> structure of language (word order, sentence structure)
- semantic -> the meaning of a sentence

Interpreter
- A component that executes the instructions contained in programs of language L
- Verður að framkvæma þær aðgerðir sem eru sértækar fyrir forritunarmálið L sem hann er að túlka
	- Aðgerðir til að meðhöndla grunntög (primitive data)
	- aðgerðir og gangaskipan til að stýra keyrsluröð aðgerða
	- Aðgerðir og gagnaskipan til að stýra gagnaflutningi
	- Aðgerðir og gangaskipan fyrir minnismeðhöndlun
- Execution cycle
	- ![Screenshot 2024-04-24 at 11.35.59.png](../images/Screenshot%202024-04-24%20at%2011.35.59.png)


Machine language
- The language L understood by the abstract machine ML's interpreter

Assembly language
- A symbolic version of the physical machine (using symbols)
- Translated into machine code using a program called the assembler

Low-level language
- Languages whose abstract machines are very close to, or coincide with, the physical machine.
	- Take into account the physical characteristics of the machine

High-level languages
- Abstract languages which ignore the physical characteristics of the computer
	- Support the use of constructs that use appropriate abstraction mechanisms to ensure that they are independent of the physical characteristics of the computer.
- Inniheldur skipan og aðgerðir til að skipuleggja gögn
	- byggt á tagkerfi (type system)
- Ef endurkvæmni er leyft er kyrrleg úthlutun minnis ófullnægjandi
- Umhverfi eitt megin einkenni, sem herma þarf í sérhverri útfærslu.
- Used to express algorithms in ways that are relatively easy for the human user to understand.

Vélbúnaður (hardware machine)
- útfærður með rökrásum og rafeindahlutum
- inniheldur
	- minni -> gögn samsett af grunttögum, runur af bitum.
	- vélarmál -> einfaldar skipanir, mengi háð undirliggjandi vél
	- túlk -> aðgerðir, vélbúnaðareiningar sem mynda örgjörvann, fetch-decode-execute

Fetch-decode-execute
- Fetch
	- næsta skipun sótt úr minni virki og þolendur geymd í instruction gisti
- Decode
	- Skipun afkóðuð með rökrásum. Þolendur sóttir með gagnaflutningaðgerðum.
- Execute
	- Grunnaðgerðir (primitive hardware operation) gagflut kemur gögnum til og frá minni.

Primitive data -> items that can be directly represented by a machine

Lexical error
- Error when turning a stream of characters into a stream of tokens.

Syntax error
- error turning a stream of tokens into a syntax tree.

1950
- First computer mainframes
- only low-level machine language used (symbolic assembly was not a thing)

Assembly langauge
- one-to-one correspondence between machine language instructions and assembly language codes
- not portable

first generation language  - 1GL -> machine language
second generation language - 2GL -> assembly language
third generation language  - 3GL -> high-level languages

FORTRAN - 50s
- The first true high-level language
- Imperative
- Numerical-scientific applications

Algol - end of 50s
- Expressing algorithms in general
- introduced blocks, recursion, type systems, BNF

LISP - 60
- The first functional language
- Fyrsta forritunarmálið til að bjóða upp 
	- endurkvæmni, föll sem fyrsta flokks þegar, ruslasöfnun
- Tög
	- Atom -> symbol og nýmerískir faster
	- Listar
- túlkurinn -> Universal fall sem ákvarðar gildi sérhvers annars falls (EVAL)
- Non-numeric applications

Scheme
- LISP mállýska -> einfaldari málskipan
- Einkenni
	- Kyrrlegar gildissviðsreglur
	- Annað sem var í LISP
- Grunnaðgerðir
	- car -> skilar haus
	- cdr -> skilar hala
	- cons -> smíðar lista
		- (list 'a 'b 'c) == (cons 'a (cons 'b (cons 'c (cons '()))))

COBOL - 60s
- Commercial applications
- Syntax closer to english

Simula - 60s
- First OO language
- Designed for simulation applications
- introduced Classes, Objects, Subtypes, dynamic method dispatch

C - 70s
- System programming language (UNIX) / general purpose
- more access to low-level functionality of the machine

Pascal - 70s
- Educational language (a simplification of ALGOL)
- first to use intermediate code for program portability
- Blcok-structured langauge

SmallTalk - 70s
- Pure object-oriented langauge
	- Everything is an object
	- Classes organized into a singly-rooted tree structure (the inheritance hierarchy)
		- Supports only single inheritance
	- Communication by sending and receiving messages
- Encapsulation, information hiding using the concepts of class & object (public vs private)
- Everything is an object
- Túlkað

ML (meta language) - 70s
- Various imperative constructs added to the purely functional part of ML
- Type checker
	- Statically determines the type of every expression in a program (no way to change it)
	- Type inference -> can deduce type without type hints

SML
- Einkenni
	- Tagályktanir
	- frábrigði
	- kyrrleg tögun
	- stranglega tagskipt
	- call-by-value
	- ADT

Prolog - 70s
- Declarative logic language - First logic programming language
- Based on the unification algorithm
- Prove a formula by explicitly computing the values of the veriables that make the formula itself true
- Programmer takes care of logic, M takes care of control
- Svar er háð flæði
	- markmið lengst til vinstri valið fyrst
	- Fyrsta viðeigandi reglar er valin fyrst
- Innsetning
	- Mengi staka á forminu X->T er innsetning (X varpað í lið T)
- Jöfnun
	- Liðir T1 og T2 geta jafnast ef T1sigma og T2sigma gefur sama tilvik fyrir innsetningu sigma
- Reglur
	- Samsvara horn klausum með visntri og hægri hlið
		- hægri (undanfari) -> margir liðir tengdir með kommu (and)
		- Vinstri (afleiðing) -> hefur einn lið
		- v <- h1 & h2 & h3 ... .
- Cuts
	- fjarlægja hluta af leitartrénu sem við viljum ekki skoða frekar
	- Beitir hvorki hopun á fyrri liði innan reglu né leitar að fleiri reglum eftir þessa.
	- force backtrack

Prolog leitart´reð
- Dregur upp mynd af þeim aðgerðum sem þarf að framkvæma til að finna allar mögulegar lausnir
	- hnútur í leitartré stendur fyrir markmið
	- Hnútur áf afkomanda fyrir hverja þá reglu sem á við hlutmarkmið lengst til vinstri í hnútum
	- flæði er rétt
- Leitar depth fyrst
	- byrja í rót
	- True í hvert sinn sem rekist er á hnút með tómu markmiði
- Getur verið óendanlegt

c++ - 80s
- C but with classes and inheritance
	- c++ objects are generalizations of C structs
- C remains a subset of c++ and is acceptable to the c++ compiler
- templates introduces -> parametric polymorphism

Ada - 80s
- Sponsored by the US department of defence
- Constructs required for programming real-time and embedded systems 
	- e.g. concurrent programming

Java - 90s
- Goal -> design based on new c++ to be used in small devices, connected to a network.
- Used to implement a kind of browser to be used for navigation through the network.
	- Portability -> JVM & bytecode
	- Security -> type safety, avoidance of explicit pointer handling


Rökforritunarmál
- setja fram þekkingu og frumsetningar um vandamálið sem nægir til að leysa það
	- Ekki röð einstakra skipanna
- Logical specifications are to all intents and purposes executable programs
- Vandamál sett fram sem markmiðssetning (goal statement) sem þarf að sanna með tilliti til frumsetninga -> útreikningur er sönnun markmiðssetningar (false ef ósannandi)
- Vensl í stað falla -> skilgreina hvaða vensl eru til (staðreyndir)
- Penalty of efficiency
	- Computation is complex -> must try various combinations of possible sublists until it finds the one that satisfies all conditions

Fallaforritunarmál
- Útreikningar án breytna eða stöðu (engar gildisveitingar)
- Útreikningar byggja á að endurskrifa segðir
	- Breytingar gerast í umvhverfinu en tengjast ekki minni.
- Endurkvæmni í stað ítrunnar
- Engin side effects -> færri lýs, order of execution irrelevant
- Grundvallaratriði
	- Abstraction, application, einsleitni
		- einsleitni as in æðri föll

Imperative programming -> gildingarforritun

Gildisveiting 
- eitt helsta einkenni hefðbundinna forritunarmála -> hægt að byggja útreikninga á breytingum á stöðu.
- Modifiable variable -> nafn sem hægt er að gefa mismuanndi gildi

Von Neumann machine
- reikingar / skipanir snúast um að breyta gildum í minnissvæðum


Declarative programming
- Paradigm that expresses the logic of computation without describing its control flow

Imperative vs. logic programming
- Imperative programming must consider logic and control
- Logic Programming only needs to consider logic -> control relegated to abstract machine -> unification


Hopun 
- When computation arrives at a point in which it cannot proceed, computation is undone so that a decision point is reached, and an alternative is chosen, or fail.

Horn clause
- Denotes reversed implication
- A program is a set or sequence of clauses (PROLOG)

Unification
- Substitutions computed so that variables and terms can be bound (or instantiated)
- Makes two sides of = equal

Tilgreind tög (explicit types)
- type hint fyrir túlkinn

Fjölvirk föll
- hægt að kalla á með viðföngum af fleiri en einu tagi

Currying
- Sérhvert fall með n viðföngum er hægt að breyta í fall með (n-1) viðföngum endurkvæmt þar til öll viðföng hafa verið fjarlægð -> hvert skilar nýju ónafngreindu falli.

Stranglega tagskipt
- Tag sérhvers nafns og segðar er hægt að ákvarða á þýðandatíma

Föll sem fyrsta flokks þegar
- geta verið útkomar úr gildi segða, geta verið stök í listum, hægt að tengja við nöfn, hægt að senda sem viðfang.
- Functions that can be treated as any other data type

Æðri föll
- Ef það getur tekið við föllum í gegnum leppa eða skilað öðru falli sem niðurstöðu (færibreyta eða skilagildi)

Föll sem skilagildi
- Gerir kleift að búa til föll á kviklegan hátt á keyrslutíma
	- Fall sem skilagildi er closure
	- Kyrrlegur hlekkur fallsins ákvarðaður með seinni hluta closure
- Vandamál
	- Hægt að skila falli sem er skilgreint inni í hreiðraðri blokk og vísar í nafn sem er í kvaðningafærslu sem var eytt

![Screenshot 2024-04-25 at 13.08.19.png](../images/Screenshot%202024-04-25%20at%2013.08.19.png)


Lambda calculus
- Hugrænt líkan til að lýsa reiknanlegum föllum
- Introduces functions as arguments
- Útreikningur með styttingu (reduction)
	- Redex -> reducible expression
		- ((fn x => body) arg)
	- Reductum af redex er segð sem fæst með því að skipta út sérhverju tilviki af leppnum í body fyrir afrit af viðfanginu
	- beta-rule (beta reduction): replace redex by reductum.

Gildisákvörðun
- (leftmost evaluation order (vinstri gildisákvörðun))
- Evaluation by value (applicative order / eager / innermost)
	- Gildið á redex er eingöngu ákvarðað ef viðfangið er þegar gildi (byrja innst)
- Evaluation by name (delayed evaluation / normal order / innermost)
	- Gildi redex ákvarðað áður en gildi viðfangsins er ákvarðað
- Lazy evaluation
	- Variation of evaluation by name
	- vista redex ef það kemur aftur upp seinna

Fallasegðir
- skila nafnlausu falli

Hugræn gagnatög (ADT)
- Gagnatag sem er skilgreint með tilliti til aðgerða á því og útfærsla þess er falin.
	- Fyrirfram skilgreind tög þar sem útfærslan er falin en forritarinn getur ekki skilgreint þess konar tög sjálfur
	- Felur útfærslu en opinberar skilin.
- Tryggja hjúpun og upplýsingahuld á gögnum og aðgerðum á skilvirkan hátt
	- Hjúpar (og sameinar) gögn og aðgerðir á þeim
- Ósveigjanlegt -> engar erfðir / engar kviklegar fjölbindingar
- Einkenni
	- Nafn tagsins
	- útfærsla
	- mengi aðgerða til að vinna með gildi tagsins -> skil
		- Nafn tags og tög aðgerða sýnileg utan frá

Hjúpun -> setja saman gögn í einn pakka ; Upplýsingahuld -> fela útfærslu

Samhæfing
- T er samhæft við S þegar allar aðgerðir á gildum af taginu S eru líka mögulegar á gildum af taginu T


Undirtög
- Tag sem tengist klasanum T er undirtag klasans S ef sérhvert boð sem hlutur af S skilur er einnig skilið af hlutum af taginu T

Undirklasi (erfðir)
- Möguleiki á að breyta skilgreiningu (útfærslu) á aðgerð sem er skilgreind í yfirklasa (yfirskrift, override)
- Annars erft af yfirklasa
- Erfðir -> hægt að skilgreina nýja klasaa með því að endurnýta

Undirtög vs erfðir
- Undirtag -> getur notað hlut í öðru samhengi án vandræða (samband milli skila)
- Erfðir -> geta endurnýtt kóða (samband milli útfærslu tveggja klasa)
- Oft tengt saman -> private erfðir í c++ er samt bara erfðir, ekki undirtag

OO mál
- Einkenni
	- útdráttur
	- undirtög
	- erfðir
	- kvikleg binding
- Klasar
	- Hjúpar gögn og aðgerðir á þeim -> býður upp á skil (interface)
	- Inniheldur
		- Meðlimaföll, tilvikabreytur, boð (fallaköll).
- Hlutir
	- Tilvik af klasa og tilheyrir þ.a.l. a.m.k. einum klasa
	- Færsla -> record sem geymir gögn, og svið fyrir aðgerðir til að meðhöndla gögnin

Útfærsla klasa
- Tengdur listi fyrir klasastigveldið
	- ![Screenshot 2024-04-23 at 17.13.40.png](../images/Screenshot%202024-04-23%20at%2017.13.40.png) Kvikleg binding
	- ![Screenshot 2024-04-23 at 20.29.29.png](../images/Screenshot%202024-04-23%20at%2020.29.29.png)
	- Kyrrleg binding
		- Rétt útfærsla á aðgerð tekur fastan tíma
		- Listi af aðgerðum geymdur í klasanum sjálfum (class descriptor)
		- Vtable í c++
		- Þegar undirklasi B af A er skilgreindur þá er vtable fyrir B búin til með því að afrita vtable fyrir A, öllum aðgerðum sem eru endurskilgreindar í B skipt út og nýjum aðgerðum í B bætt við
		- Kalla á tilvikaaðgerð kostar að fylgja tveimur bendum 

Hlutur vs. ADT
- þegar ADT breyta er skilgreind þá stendur hún aðeins fyrir þau gögn sem hægt er að meðhöndla með aðgerðum
- sérhvert tilvik af klasa er gámur sem raunverulega hjúpar bæði gögn og aðgerðir

Klasabreytur og klasaaðgerðir
- Tengja breytur og aðgerðir við klasann frekar en tilvik
- Geymdar í klasanum með meðlimaföllum -> meðlimaföll taka tilvik sem inntak.

Kvikleg binding (dynamic binding)
- Þýðandi getur ekki ákvarðað tag á hlut fyrr en á keyrslutíma
- Tryggir að kallað verði á réttu aðgerðina fyrir sérhvert tilvik
- Þegar boð m er sent til hlutar o þá geta verið margar útgáfur af útfærslu á m fyrir o -> val á útfærslu er háð tagi hlutsins sem fær boðin.

Gagnatag
- einsleitt (homogenous) safn gilda með skilvirka skipan, búið mengi aðgerða til að meðhöndla gildi.
- ástæður
	- hönnunarstig   -> conceptual organization
	- forritunarstig -> réttleiki (tagskoðun / type checking)
	- þýðingarstig   -> stuðningur við útfærslu

Tagskoðari
- Ákvarðar hvort tagskilyrðum (type constraints) sé fullnægt fyrir keyrslu
- hluti af þeim fasa þýðanda sem sér um að skoða setningafræðileg skilyrði háð samhengi (contextual syntax checking)

Tög -> controlled comments
- Gefa til kynna hvernig hlutir eru notaðir (á löglegan hátt)
- Sýndarvélin finnur ranga notkun á þessum hlutum
	- Mikilvægar upplýsingar fyrir sýndarvél
	- segir til um
		- stærð í minni
- Getur verið takmarkandi


Kyrrleg tögun
- þegar tög eru til staðar í forritskóða þá eru upplýsingar sem þessar aðgengilegar á þýðingartíma.
- Kyrrleg úthlutun minnis við þýðingu er möguleg -> bestar aðgerðir
- Aðgangur að breytu í kvaðningafærslu er útfærð með offset frá bendi á kvaðningafærslu.

Tagkerfi (type system)
- mengi af fyrirfram skilgreindum tögum í málinu
- Upplýsingar um hvort tagskoðun er kyrrleg eða kvikleg
- Aðferðir við að stýra tögun
	- Jafngildisreglur -> hvenær tvö mismunandi tög eru jafngild
	- Samhæfisreglur -> hvenær gildi tags getur verið notað í öðru samhengi 
	- Reglur og aðferðir við tagályktun -> hvernig úthluta tagi flókin segð

Stranglega tagað mál (strongly typed langauge)
- Type safe langauge
- Þegar ekkert forrit getur í keyrslu framkallað unsignalled villu sem má rekja til tagvillu
- (type casting í c++ -> ekki stranglega tagað (framkallar villu á keyrslutíma))

Kyrrleg tagskoðun (á þýðandatíma)
- Kostir
	- villur tilkynntar um leið og forritið er þýtt
	- Utanumhald um tög á keyrslutíma óþarfi -> réttleiki tryggður fyrir þýðingu
	- Betri skjölun -> tög sýnileg notendum
- Ókostir
	- hönnun kyrrlega tagaðra mála flóknari (sérstaklega ef type safe)
	- þýðing flóknari og tekur lengri tíma
- C, C++, Java

Kvikleg tagskoðun (á keyrslutíma)
- Sérhver hlutur hefur run-time-descriptor sem tilgreinir tag þess
	- tagskoðun með tagskoðunarkóða sem keyrður er á undan sérhverri aðgerð
- Kostir
	- Sveigjanleiki fyrir forritarann
	- Fljótari þróunartími
	- betri tjáningarhæfni
- Ókostir
	- hægari keyrsla (overhead) 
	- Villa kemur ekki fram fyrr en á keyrslutíma
- Python, Ruby, Perl

Gagnaútdráttur
- Flest forritunarmál hafa fyrirfram skilgreind tög og leiðir til að skilgreina ný tög (samsett tög)

Abstraction mechanisms
- Ferlaútdráttur
	- Gerir kleift að fela nákvæma virkni tiltekins ferlis (falls)
- Gagnaútdráttur
	- Gerir kleift að nota gagnatög án þess að vísa í hvernig tögin eru útfærð

Stikar (parameters)
- Leppar (formal parameters)
	- Koma í skilgreiningu á falli
	- haga sér eins og staðværar skilgreiningar
- Viðföng (acutal parameters)
	- koma fyrir í fallakalli

Fall
- kóðabútur auðkenndur með nafni
- Á eigið staðvært umhverfi
- Skiptir á upplýsingum við aðra hluti gegnum
	- Stika (parameters)
	- skilagildi (return value)
	- non-local environment

Procedure
- Undirforrit sem hefur samskipti við caller eingöngu gegnum stika að nonlocal umhverfi -> ekkert skilagildi

Aðferðir við stikun færibreytna
- (Hernig viðföng eru pöruð við leppa og merkingin sem tengist því)
- Call by value
	- Bara r-value (gildi) tengt við lepp 
	- Leppur á sér minnissvæði í kvaðningafærslu callee
- Call by reference
	- Færibreyta getur verið notuð fyrir inntak og úttak
	- tengsl mynduð milli lepps og l-value viðfangsins (aliasing)
	- Leppur á minnissvæði í kvaðningafærslu fallsins (geymir bendi)
	- hraðvirkt
- Call by result
	- output-only aðferð
	- viðfang verður að vera segð með l-value
	- Þegar fall hættir keyrslu er núverandi gildi leppsins afritað fyir í l-value viðfangsins
	- engar upplýsingar færðar frá caller í callee
- Call by value-result
	- Samsetning call by value og call by result -> bidirectional communication
	- Í byrjun er r-value afritað í lepp
	- í lok er r-value lepps afritað í l-value viðfangs

l-value
- gildi sem stendur fyrir minnissvæði

r-value
- gildi sem hægt er að geyma í minnissvæði, gildi segðar hægri hlið gildisveitingar

Tegundir bindinga fyrir æðri föll
- (möguleikar til að velja non-local umhverfi þegar kallað er á fall f sem er með lepp (fall) h)
- Deep binding
	- Nota umverfið sem er virkt á þeim tíma þegar tenging milli lepps og falls er búin til
	- Alltaf notað í kyrrlegum gildissviðum.
	- Kyrrlegur bendir ákvarðaður þegar tengsl milli lepps og viðfangs eru mynduð.
	- Útfærsla
		- Leppurinn tengdur við Closure: par af tilvísunum (kóði, kvaðningafærsla)
			- Kóði -> færir flæði forritsins í rétt fall
			- kvaðningafærsla -> gefur kyrrlega hlekknum í nýju kvaðningafærslunni það gildi
- Shallow binding
	- Nota umhverfið sem er virkt þegar kallað er á fallið með h sem viðfang á sér stað


Endurkvæmni
- Sérhvert fallakall þarf á eigin minnissvæði að halda til að geyma upplýsingar
- Kyrrleg úthlutun minnis er ekki nægjanleg
- Kvikleg úthlutun minnis og deallocation nauðsynleg á keyrslutíma
	- Keryslustaflinn
	- Heap notað þegar setning í forriti biður um úthlutun á kviklegu minni

Kyrrleg minnismeðhöndlun
- Einkenni
	- Framvkæmd af þýðandanum áður en keyrsla forrits hefst
	- Hlutir sem úthlutað er í kyrrlegu minni eru geymdir í fyrirfram skilgreindu svæði í minni og eru þar á meðan forritið keyrir
		- Víðværar breytur, vélarmálskóði, töflur sem þýðandinn býr til
- Ef forritunarmál leyfir EKKI endurkvæmni þá er hægt að úthluta minni fyrir staðværar byretur falls á kyrrlegan hátt.

Kvikleg minnismeðhöndlun með stafla
- Komið er inn og út úr blokkum með LIFO -> stafli notaður til að halda utan um minni sem er staðvært í sérhverri blokk.
- Keyrslustafli -> geymir kvaðningafærslur á keyrslutíma

Meðhöndlun staflans -> caller & callee -> gert af þýðanda
- Calling sequence
	- Kóði í caller sem keyra þarf að hluta til áður en kall á sér stað og að hluta til eftir á
- Prologue
	- Keyrt af callee strax eftir fallakall
- Epilogue
	- keyrt af callee þegar fallið hættir keyrslu

Deallocation -> að fjarlægja kvaðningafærslu af staflanum

Kvaðningafærsla
- Settar og fjarlægðar af stalfanum á keyrslutíma
- Minnissvæði á keyrslustaflanum sem tilheyrir "in-line"blockk eða kvaðningu falls -> tengist þeirri kvaðningu og er búin til við fallakall / enter á block
- fyrir "in-line" block
	- Milliniðurstöður
	- staðværar breytur -> þýðandi ákvarðar stærð þessa hluta kvaðningafærslu
	- Kviklegur bendir (dynamic chain pointer)
		- Bendir á kvaðningarfærsluna sem er næst á undan á staflanum.
- Fyrir föll
	- Milliniðurstöður
	- Staðværar breytur
	- Kviklegur bendir
	- Kyrrlegur bendir -> uppl nauðsynlegar til að útfæra kyrrlegar gildissviðsreglur
	- Afturhvarfsvistfang (return address) -> vistfang á fyrstu skipun eftir fallakall
	- Skilagildi -> minnissvæði í kvaðningafærslu caller
	- Viðföng -> gildi viðfanga notuð í fallakalli


Kviklegur bendir
 - Bendir á tiltekið fast svæði nálægt miðju í kvaðningafærslu á undan
 - Vistföng á mismunandi sviðum fengin með því að bæta offset við gildið á kviklegum bendi
 - Þýðandi skiptir út tilvísun í staðværar breytur fyrir vistföng miðað við offset í kvaðningafærslunni

Gildissviðsreglur
- Kyrrlegar
	- byggt á texta forrits (blokkir) -> háð því
	- Getur verið ákvarðað af þýðanda
	- kostir
		- Hægt að sjá tengingar beint í kóða
		- þýðandi skilur og þar með hægt að testa á þýðandatíma (tagskoðun t.d.)
- Kviklegar
	- Byggt á flæði á keyrslutíma
	- Nýjustu tengsli sem búin voru til fyrir nafn og er enn virk (á stafla)
	- kostur -> sveigjanleiki
	- óksotir
		- erfitt að lesa forritið með tilliti til keyrslusvæðis
		- óskilvirkara í keyrslu samanborið við kyrrlegt gildissvið


Útfærsla á gildissviðsreglum
- Tilvísun í non-local nafn
	- Þarf að skoða kvaðningafærslur á staflanum til að finna þá sem á nafnið
	- Kyrrleg keðja
		- Kyrrlegi hlekkurinn notaður til að finna færsluna -> endurspeglar strúktúr á hreiðruðum (nested) blokkum í forritinu
		- Levels of nesting eftir kyrrlegu keðju (reiknanlegt kyrrlega)
	- Kviklegi bendirinn
		- leita að tilvísunum í non-local breytu
		- Nöfn breytna þarf að geyma í kvðaningafærslu (eða external gsk)

Umhverfi
- mengi af tengslum milli nafna og merkjanlegra hluta sem er til staðar á keyrslutíma á ákveðnum stað og tíma í forritinu er kallað tilvísunarumhverfi
- Tegundir
	- Staðvært
		- leppar + mengi tengsla fyrir nöfn sem skilgreind eru innan blokkar
	- "non-local"
		- tengsl fyrir nöfn sýnileg inni í blokk en yfirlýst utan hennar
	- Víðvært
		- hægt að nota í öllum blokkum forrits
		- Mengi nafnatengsla lýst yfir þegar forrit hóf keyrslu

Blokkir
- Textasvæði í forritinu merkt með start og end tákni
- getur innihaldið yfirlýsngar sem eru staðværar (innan umrædds svæðis)
- tegundir
	- tengd falli (yfirlýsingu -> body + leppar)
	- in-line -> (ekki yfirlýsing á falli)

Sýnileikaregla -> seinast skilgreint í keðju, nota það.

Ofansækinn endurkvæmnisþáttari (recursive descent parser)
- Safn endurkvæminna undirforrita sem byggir þáttunartré á ofansækinn máta
- Undirforrit fyrir sérhverja máleiningu í mállýsingu
- Tré byggt í pre-order frá rót og niður að laufum (vinstri afleiðsla)

Neðansækinn endurkvæmnisþáttari
- byggt frá laufum upp í rót.

Parsin decision problem -> velja reglu til að beita, nota fyrstu mögulegu tóka (oftast)

LL málfræðiflokkur
- left to right scan & leftmost derivation
- Ekki hægt að skrifa LL þáttara fyrir allar mállýsingar
- A -> A + B t.d.

Þýðendur skipta greiningu málskipan
- Lesgreining
	- Les einstaka stafi sem mynda forritstextann og tekur saman í merkingarbærar einingar.
	- Lexical error
	- Meðhöndlar tóka (litlar máleiningar)
		- nöfn, tölur, virkar, greinarmerki
- Þáttun
	- Athugar hvort runa tóka mundi löglega setningu
	- Syntax error
	- Meðhöndlar stærri máleiningar
		- segðir, setningar, forritunareiningar.

![Screenshot 2024-04-23 at 23.43.14.png](../images/Screenshot%202024-04-23%20at%2023.43.14.png)

Lesgreinir (lexical analysis)
- leitar að mynstrum í texta -> finnur hlutstrengi sem passa við mynstur
- Safnar stöfum í lógíska röð -> stafaraðir kallast les (lexeme) táknaðir með tókum (kóði fyrir flokkun)
- Finnur les og skilar til þáttara -> sleppir óþarfa jukki
- Endanleg stöðuvél sem ber kennsl á flokk mála sem kallast regluleg mál

Þáttun (syntax parsing)
- Markmið
	- Athuga hovrt forrit er setningafræðilega rétt
	- Búa til þáttunartré (stundum óbeint)

Leiðir til að lýsa máli
- málfræði
	- hvaða orð / setningar / frasar eru réttir -> lesgreining
	- Málskipan -> hvaða röð af tókum mynda löglegar setningar (CFG)
- merking
	- Hvaða merking liggur í löglegri setningu
- málnotkunarfræði (pragmatics)
	- Hvernig notum við merkingarbærar setningar
- Útfærsla
	- Hvernig keyrum við löglega setningu þannig að tekið sé tillit til merkingar

Context free grammar (samhengisfrjáls mállýsing)
- Aðferð til að lýsa setningarfræðilegum fyrirbærum á formlegan hátt (Noam Chomsky)
- fernd G = {NT, T, R, S} 
	- NT -> mengi non-terminals
	- T -> mengi terminals
	- R -> mengi reglna (productions), hver á forminu V->w
	- S -> stak í NT (start symbol)
- Mál -> L(G) = { w € T* | S=\*> w}

Þáttunartré
- Lægra í trénu = meiri forgangur
- Margræðni -> ef til er a.m.k. einn strengur í L(G) sem hægt er að mynda með fleiri en einu þáttunartré (ónothæf lýsing á forritunarmáli)

Setningafræðileg skylirði háð samhengi
- Strengir löglegir m.t.t. mállýsingar aðeins löglegir í réttu samhengi

Samhengisháð mállýsing (context-sensitive grammar)

Raunstikar / viðföng -> actual parameters
Lepper -> formal parameters

Þýðandi
![Screenshot 2024-04-24 at 11.10.53.png](../images/Screenshot%202024-04-24%20at%2011.10.53.png)


Merkingargreining (semantic analysis)
- Þáttunartréð notað til að tékka ýmis samhengisháð skilyrði í málinu
	- Skreytt merkingarfræðilegum upplýsingum
	- Tóki sem stendur fyrir breytu er skreyttur með tagi
	- uppl um breytur geymdar í nafnatöflu (gangaskipan)

Myndun milliþulu (intermediate code)
- Fyrsti fasi þulusmíðinnar (code generation) (code that can be readily executed by the target system)
- Þula ekki búin til því hægt að besta
- Milliþula óháð bæði frummáli og markmáli

Þulubestun
- bestun áður en smíði þulu í markmáli á sér stað
	- fjarlægja ónotaðan kóða
	- in-line expansion af function calls
	- bestun á lykkjum.

Þulusmíði
- þula í markmáli mynduð út frá milliþulu sem hefur verið bestuð
- síðasti fasi bestunar háður eiginleikum markmáls / vélbúnaðar
- í þýðanda + register assignemtn




















--------



![Screenshot 2024-04-25 at 18.50.58.png](../images/Screenshot%202024-04-25%20at%2018.50.58.png)![Screenshot 2024-04-25 at 18.54.24.png](../images/Screenshot%202024-04-25%20at%2018.54.24.png)![Screenshot 2024-04-25 at 18.54.44.png](../images/Screenshot%202024-04-25%20at%2018.54.44.png)

Prolog algrímið notar eftirfarandi aðferð þegar það leitar að lausn við fyrirspurn:
Reynt er að sanna hlutmarkmið (e. subgoal) frá vinstri til hægri og ef fleiri en ein regla á við tiltekið hlutmarkmið þá eru þær valdar í þeirri röð sem þær birtast í forritskóðanum

Scheme er kviklega tagað (e. dynamically typed) en ML er kyrrlega tagað (e. statically typed).

Scheme er kviklega tagað (e. dynamically typed) en ML er kyrrlega tagað (e. statically typed).

Í evaluation by value er gildi viðfangs (segðar) fyrst ákvarðað áður en kallað er á fallið og leppnum skipt út fyrir það gildi en í evaluation by name er viðfangið sett óbreytt inn fyrir leppinn og gildi segðarinnar ákvarðað síðar.


Af hverju er Java ekki "hreint" (e. pure) hlutbundið forritunarmál?
Því grunntög í Java eru ekki hlutir (e. objects)

Ekki þarf að halda utan um kyrrlega keðju (e. static chain) og til að senda fall f sem viðfang í annað fall er nægjanlegt að senda bendi á kóða fallsins f.


Kostir milliþulu
- Hana er hægt að nota til að þýða endanlega yfir á fleiri en eitt tiltekið markmál
- Hún brúar bilið á milli "high-level" frummáls (e. source language) og "low-level" markmáls (e. target language)



Túlkur fyrir forritunarmál L er notaður til að:
- Sækja, afkóða og keyra eina skipun í einu í forriti í L

Hvernig er rétta “non-  
local” breytan  
(minnishólf) fundin á  
keyrslutíma  
How is the correct non-  
local variable (memory  
location) found at run-  
time  
### Kyrrlegar gildissviðs
A reference to a non-local  
variable can be statically  
computed (chain_offset,  
local offset) and no search  
is therefore carried out at  
run-time to find the  
variable. The chain_offset  
stands for the number static  
chain links that need to be  
travelled to find the correct  
activation record.  
#### Kviklegar gildissviðs
A reference to a non-local  
variable cannot be  
statically computed, and a  
search in activation records  
is carried out by travelling  
through the dynamic chain  
to find the newest  
occurance of the named  
variable

| s f c|  
Transcript show: ' Enter a line: '.  
s := stdin nextLine.  
f := Bag new.  
s do: [ :ch | ch isLetter  
ifTrue: [ f add: ch asLowercase]  
].  
1 to: 26 do: [ :i |  
c := (i+96) asCharacter.  
Transcript show:((f occurrencesOf: c) printString, ' ')  
]  
a) (2%) Hvaða klasaaðgerðir koma fyrir í kóðanum? / Which class methods  
appear in this code?  
show:  
new:  
b) (4%) Hvaða tilvikaaðgerðir koma fyrir í kóðanum? / Which instance methods  
appear in this code?  
nextLine  
do:  
add:  
isLetter  
ifTrue:  
asLowercase  
to:do:  
asCharacter  
occurrencesOf:  
printString  
+  
,  
c) (2%) Hvert er úttak forritsins miðað við inntakið “Smalltalk is an elegant  
language!” / What is the output of the program given the input “Smalltalk is an  
elegant language!”  
a b c d e f g h i j k l m n o p q r s t u v w x y z  
6 0 0 0 3 0 3 0 1 0 1 5 1 3 0 0 0 0 2 2 1 0 0 0 0 0