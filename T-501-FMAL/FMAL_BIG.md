
------


Abstract machine
- closely related to programming lanaguages
- how to describe an implementation of a programming language
- An abstraction of the concept of a physical computer
- An abstract machine for the programming language L, denoted with ML, is any set of data structures and algorithms which can perform the storage and execution of programs written in L.
- Generic abstract machine is composed of 
	- a store
		- serves to store data and programs
	- an interpreter
		- the component that executes the instructions contained in programs
- A device which allows the execution of programs written in L
- Differences between them derived from implementation of interpreter and data structures used
- Implementations
	- in hardware
		- using physical devices (memory, arithmetic and logic circuits, etc.) to implement a physical machine whose machine language coincides with L
		- Sufficient to implement in hardware the data structures and algorithms constituting the abstract machine
		- Fast -> directly executed by hardware
		- Very complicated to do for high level languages
		- impossible to modify afterwards
		- mostly, only low-level languages used
	- simulation in software
		- impplement data structures and algorithms required by ML using programs written in another language L' (which has already been implemented)
		- greatest flexibility
		- lower performance (interpret twice or more times)
	- simulation (emulation) using firmware
		- Emulation of the data structures and algorithms for ML in microcode.
		- higher execution speed than normal software simulation
		- less flexible
			- re-writing requires special hardware
		- intermediate between hardware and software implementation

Hierarchies of abstract machines
- Hierarchies that desribe and implement complex software system


Programming language
- Algorithms must be appropriately formalised using the constructs provided by a programming language
- Formally defined in terms of a specific syntax and a precise semantics
- Implementing a programming language L means implementing an abstract machine which has L as its machine language


A program
- a finite set of instructions of a language L
- are data to interpreters


Computing machine
- executes algorithms which are suitably formalised so taht the machine can understand them


Interpreter
- A component that executs the instructions contained in programs of language L
- Types of operations executed by interpreters
	- Operations for processing primitive data (primitive operations)
		- Primitive data -> items that can be directly represented by a machine (integers / real numbers)
			- Arithmetic operations 
	- operations and data structures for controlling the sequence of exeuction of operations
		- Allowing us to control the exeuction flow of instructions in a program
		- needs data structure to store hold address of next operation, and manipulate them with special instructions (different from those used for data manipulation
		- e.g. change control flow based on condition / input
	- operations and data structures for controlling data transfers
		- Control how operands and data is to be transferred from memory to the interpreter and vice versa.
	- operations and data structures for memory management.
		- Operations used to allocate data and programs in memory
- Interpreter's execution cycle (fetch-decode-execute cycle)
	- substantially the same for all interpreters (jmp pg. 21)
	- fetch next instruction to execute from memory
	- decode instruction to determine operations to be performed as well as operands
	- operands fetched from memory
	- The instruction (one of the machine's primitvies, is executed
	- once completed, results are stored)
	- unless halt instruction is invoked, continue the cycle
- An interpreter forthe hardware machine is implemented as a set of physical devices which comprise the control unit and which support execution of the fetch-decode-execute cycle


machine language
- the language L understood by the Abstract Machine ML's interpreter
- The internal representation of the programs executed by the machine ML is usually different from its external representation.


Compiler


Low-level languages
- Languages whose abstract machines are very close to, or coincide with, the physical machine
- Take into account the physical characteristics of the machine
	- overhead when writing algorithms
- A particular low-level language for a physical machine is its assembly language
	- A symbolic version of the physical machine
		- uses symbols such as ADD, MUL, etc. instead of binary codes
	- Translated into machine code using a program called an assembler

high-level languages
- Languages that support the use of constructs that use appropriate abstraction mechanisms to ensure that they are independent of the physical characteristics of the computer.
- suited to expressing algorithms in ways that are relatviely easy for the human user to understand


CISC
- many machine instructions

RISC
- Fewer instructions, which are simple enough to be executed in a few (or one) clock cycle in pipelined fashion


**The lexical error vs.** **syntactic error is a bit more difficult**. Long story short, lexers (which have lexical errors) turn a stream of characters into a stream of tokens, while parsers (which have syntax errors) turn a stream of tokens into a syntax tree. 

---


First computers (mainframes) appeared around 1950
- only low-level machine language used
- Symbolic assembly code was not even a concept

Assembly languages
- introduced as a step away from machine languages towards user's natural language
- Symbolic representations of the machine language
- one-to-one correspondence between machine language instructions and assembly language codes
- not portable -> every computer has its own assembly language

Assembler
- translates an assembly language program into machine language





high-level language
- Abstract languages which ignore the physical characteristics of the computer
- FORTRAN -> the first true high-level language

FORTRAN
- imperative language
- Designed for applications of a numerical-scientific type
- Still used for some numerical applications

ALGOL
- suited to expressing algorithms in general, rather than for use in specific types of application
- Introduced many concepts found in modern languages
	- Blocks
	- Recursion
	- Type system
	- BNF

LISP (list processor)
- the first functional language
- Designed for non-numeric applications
	- Symbolic expressions and artificial intelligence
- Contributed
	- higher-order functions
	- dynamic memory management (using heap)
	- automatic garbage collection

COBOL (common business oriented language)
- Designed for commercial applications
- syntax close to English


SIMULA
- first OO language
- designed for simulation applications
- introduced
	- Classes
	- Objects
	- Subtypes
	- dynamic method dispatch

C (the system programming language)
- Designed as a system programming language for UNIX
- more opportunities to access the low-level functionality of the machine and to program interactive systems than its predecessors
- General purpose language
- C does not allow nested functions

Pascal (educational langauge)
- simplicfication of ALGOL
- introduced the concept of intermedidate code as an instrument for program portability
- Block-structured langauge in which it is possible to define functions and blocks that can be nested with arbitrary complexity

SmallTalk
- the "true" object oriented language
- Presents programming language mechanisms for encapsulation and information hiding using the concepts of class and object
	- Precice visibility rules for classes (public vs private)
- Everything is an object
- A total system which includes a
	- language
	- programming environment
	- special dedicated machine for program execution

ML (meta language)
- various imperative constructs added to the purely functional part of ML
- important contributions
	- type checker statically determines the type of every expression in a program and there is no way to change this type
	- ML type system supports a type inference mechanism
		- programmer leaves some information about types unspecified and the system, using a form of logical inference deduces the tyep of the identifiers from the way in which they are used.

PROLOG
- Declarative logic language
- The first logic programming language
- based on the unification algorithm
- Allows to prove a formula by explicitly computing the values of the variables that make the formula itself true
- programmer takes care of the logic, the abstract machine (prolog interpreter) takes care of the control

C++
- 1980s
- Classes and inheritance added to the C language without compromising efficiency and compatibility with the existing C langauge
- C remains a subset of c++ and as such has to be accebtable to the C++ compiler
- templates added -> parametric polymorphism
- c++ objects are a generalization of C structs

Ada
- Sponsored by the US department of defense
- Introduces many new constructs required for programming real-time and embedded systems
- Concurrent programming

Java
- 1990s
- Goal of defining a language, based on a new implementation of C++ to be used in small computing devices with relatively limited power, connected to a network.
- used to implement a kind of browser to be used for navigation through the network
- Two important design requirements
	- portability -> java virtual machine and associated byte code
	- security    -> Type safety, avoidance of explicit pointer handling


The Prolog algorithm
- Algorithm = logic + control
- Flæði í prolog (svar er háð flæði)
	- röð markmiða (goal order) 
		- markmið lengst til vinstri er valið fyrst
	- röð reglna (rule order)
		- Fyrsta viðeigandi regla er valin fyrst
- Jöfnun og innsetning (unification and instantiation)

Innsetning
- Mengi staka á forminu X -> T er innsetning
	- breytunni X er varpað yfir í lið T
- Tsigma stendur fyrir beitingu innsetningar sigma á lið er 
	- Xsigma = U if X -> U is in sigma
	- Xsigma = X if X->U is not in sigma
	- (f(T1, T2)) sigma = f(U1, U2) if T1sigma = U1, T2sigma = U2
- Liður U er tilvik af T ef U = Tsigma fyrir einhverja innsetningu sigma
- Liðir T1 og T2 geta jafnast (unify) ef T1sigma og T2sigma gefur sama tilvik fyrir innsetningu sigma
	- jafnari fyrir T1 og T2

Prolog letiartré
- dregur upp mynd af þeim aðgerðum sem þarf að framkvæma til að finna allar mögulegar lausnir við fyrirspurn
	- Hnútur í leitartré stendur fyrir markmið
	- Hnútur á afkomanda fyrir hverja þá reglu sem á við hlutmarkmið lengst til vinstri í hnútum.
	- Röð afkomenda er sú sama og sú röð sem reglurnar eru settar fram í.
- Leitar depth fyrst
	- Byrja í rót
	- Hluttré afkomanda hvers hnútar eru skoðuð frá vinstri til hægri
	- Niðurstaðan er true svar í hvert sinn sem prolog rekst á hnút með tómu markmiði
- Endanlegt vs. óendanlegt leitartré
- Sumt getur aldrei fundið lausn ef base caseið er ekki fremst í röð reglnanna

Prolog
- setningar samanstanda af liðum (terms)
	- liður
		- fasti, breyta, eða strúktúr
	- Fasti er annað hvort atom eða tala
- Breytur eru taglausar
	- Binding breytu vil gildi er kallað instantiation
	- Gildir eingöngu meðan verið er að sanna / afsanna fullyrðingu
- Strúktúr stendur fyrir vensl / umsögn)
- Staðreyndir
	- Notaðar til að byggja upp gagnagrunn af fullyrðingum sem gert er ráð fyrir að séu sannar
	- Engin innbyggð merking í staðreyndum
	- samsvara horn clauses með tóma hægri hlið
	- Basically base case -> ef nær þessu þá true
- Reglur
	- samsvara horn clauses með vinstri og hægri hlið
	- if hægri then vinstri
		- hægri hlið er undanfari (antecedent)
			- hefur marga liði tengda saman með kommu (samtenging / and)
		- Vinstri hlið er afleiðing (consequent)
			- hefur eingöngu einn hlið
- Markmið (fyrirspurn, goal, query)
	- someFunction(X, bill) -> Prolog reynir að finna jöfnun með instantiation á X sem veldur því að niðurstaaða fyrirspurnarinnar er true
- listar í prolog
	- \[H|T] head og tail
- Guess and verify (generate and test) fyrirspurn
	- er til x þannig að someFunc1(s) og someFunc2(S) eru subgoal
	- Finna S þannig að someFunc1 og someFunc2 eru sannar

Hopun (backtracking)
- return to a marked palce and try to re-satisfy
- e.g. finna lausn fyrir fyrri part af and, finnur ekki lausn fyrir seinni, og heldur því áfram að leita á sama stað á fyrri partinum


Cuts (prolog) !
- Fjarlægja hluta af leitartrénu sem við viljum ekki skoða frekar
- gerir leit skilvirkari með því að fjarlægja óþarfa leið eða stoppa hopun
- líka hægt til að útfæra neitun 
- Stoppar hopun
- Klippir hluta af leitartrénu af
- case
	- ef b false
		- halda áfram og reyna klausu nr k + 1
	- ef b true
		- ! er ákvarðað (alltaf true)
		- ferlið heldur áfram með C
		- ef hopun á sér stað þá eru allir aðrir möguleikar varðandi ákvörðun á B fjarlægðir, svo og allir möguleikarnir sem fólgnir eru í klausum k + 1 til n til að ákvarða p(t)

![Screenshot 2024-04-23 at 12.19.19.png](../images/Screenshot%202024-04-23%20at%2012.19.19.png)


Rökforritunarmál
- setja fram þekkingu og frumsetningar um vandamálið sem nægir til að leysa það
- ekki röð einstakra skipanna
- Vandamál er þá sett fram sem markmiðssetning (goal statement) sem þarf að sanna með tilliti til frumsetninga
- útreikningur == sönnun markmiðssetningar
- Algorithm = logic + control
- Vinna með vensl (umsagnir) í stað falla
	- sveigjanlegri
	- vensl meðhöndla viðföng og svör á sama hátt
	- engir fordómar um hvað sé reiknað út frá hverju
	- talfa með n dálkum og hugsanlega óednanlegum fjölda raða
	- Vensl er í raun test (er gefin færsla í venslunum v)
		- Vensl eru skilgreind með reglum p er satt ef Q1 og Q2, og Q3
			- horn klausa
			- í horn klausu væru engin condition (gildi án skilyrða)
- Breytur byrja á stórum staf
- atom stendur fyrir jsálft sig (litlir stafir)
- False ef getur ekki verið sannað
	- Fyrirspurn er false ef Prolog getur ekki beitt afleiðslu til að sanna P út frá frumsetningum
- = stendur fyrir jöfnun X = 2+3
- X is 2+3 -> reiknar


Stefjuforritun
- algorithms + data structures = programs


Prolog (programmation en logique)
hannað fyrir málvinnslu (natural language processing)


Declarative programming
- a programming paradigm the expresses the logic of a computation without describing its control flow
	- SQl, REGEX, functional and logic programming languages

Deduction as computations
- Algorithm = Logic + control
	- logic is what must be done
	- control is how the desired solution is found


imperative vs. logic languages
- Imperative programming must consider both logic and control
- Logic programming only needs to consider the logic
	- control is relegated to the abstract machine
	- unification forms the basic computational mechanism of logic programming languages

Logic programming
- the logical specifications are to all intents and purposes executable programs
- Specification can be read in a procedural fashion
- Penalty of efficiency
	- Computation is complex
	- Abstract machine must try the various combinations of possible sublists until ti finds the one that satisfies all the conditions
	- use backtracing
	- This search process can have exponential complexity
- use first-order logic (predicate calculus (umsagnarreikningur))


Hopun Backtracking
- when the computation arrives at a point at which it cannot proceed, the computation that has been performed is undone so that a decision point can be reached (if it exists) then an alternative is chosen (or fail if that doesn't exist)

First-order logic
- consists of three components
	- an alphabet
		- set of logical 
			- and, or, not, implication, logical equivalence, true, false, exists, for all, and an infinite set of variables
		- set of non-logical symbols
			- Function (sum) and predicate symbols () relations
	- terms defined over this alphabet
	- well-formed formulæ defined over this alphabet

Liðir (terms)
- Terms over a signature Sigma (and over the set V of variables) are defined inductively as follows
	- A variable (in V) is a term
	- if f (in sigma) is a function symbol of arity n and t1, ..., tn are terms, then f(t1, ..., tn) is a term
- Constant is a term
- f(a,b) would also be a term

Well-formed formulæ
- allow us to express the properties of terms
	- E.g. given the predicate >, writing > (3,2) we want to express the fact that the term 3 corresponds to a value which is greater than that associated with the term 2
- Predicates can be used to construct complex expressions using logical symbols

Clauses
- a particular class of formulæ
- more efficient manipulation using a special inference rule called resolution
- Definite clause -> a restricted version of the concept of clause
- definite clause (horn clause): let H, A1, ... An be atomic formulæ. A definite clause is a formula of the form H :- A1,... An
	- if n = 0 -> fact and :- is omitted
	- otherwise query or goal

Horn clause 
- H:- A1, ... An
- :- denotes reversed implication <-
- The commas in a clause or query denote a logical conjunction
	- right -> body
- A program is a set or sequence of clauses


Unification
- Substitutions computed so that variables and terms can be bound (or instantiated)
- The fundamental computational mechanism in logic programming is the solution of equations between terms using the unification procedure
- The computation of different substitutions obtained in the course of a computation provides the result of the calculation


Logic variable
- an unknown which can assume values from a predetermined set
- can be bound only once
- value can be partially defined to be specified later
- binding for logic variables can have bidirectional nature

Substitution
- Connection between variables and terms is made in terms of the concept of substitution, which allows the substitution of a variable by a term
- A substitution is a function from variables to terms such that the number of variables which are not mapped themselves is finite
- v = {X1/t1, ... Xn/tn}
- Application of substitutions
	- if we consider an expression E, the result of the application of v to is (Ev) is obtained by simultaneously replacing every occurrence of Xi in E by the corresponding ti for all 1 <= i <= n

Unification
- if a substitution makes the two sides of = equal
- f(X) = f(g(Y)) with v = {X / g(Y)}
- most general unfiier -> m.g.u. f X is the one that cannot accept more substitutions within itself (least work)
- The problem of determining whether a set of equations of terms can be unified is decidable


SML -> standard ML (meta language)
- Einkenni
	- tagskilgreiningar (type declarations)
	- tagályktanir (type inference)
		- if x and y are int then x + y is int
	- tilfelli og mynstur (cases and patterns)
	- modules
	- frábrigði (exceptions)
	- kyrrleg tögun (static typing)
	- stranglega tagskipt (strongly typed)
		- tag sérhvers nafns og segðar er hægt að ákvarða á þýðandatíma
	- call-by-value
	- Styður hugræn gagnatög (abstract data types)
- Listar
	- röð 0 eða fleiri staka af sama tagi innan \[] með kommu milli staka
	- annað hvort
		- ö[], nil (tómur)
		- a::y -> a er haus, y er hali (listi)
	- Listaaðgerðir
		- null(x) -> true if x is an empty list
		- hd(x)   -> head of x
		- tl(x)   -> tail of x
		- a::x    -> construct list with head a and tail x
- Föll
	- fun functionName parameters = body
	- segð f g x er jafngild (f g) x
	- fallakall
		- f(x) eða f x
	- Flest listaföll meðhöndla lista stak fyrir stak (LÍNULEGA ENDURKVÆM
	- append(x, y) = x @ y = x::y (seinasta smá bull btw)
	- rev(x)
- Tilfelli og mynstur
	- t.d. listaföll
		- yfirleitt tvö tilfelli
			- eitt fyrir tóma listann og annað fyrir lista sem er ekki tómur
			- e.g.
				- lengt(\[]) = 0
				- length(a::y) = 1 + length(y)
	- case -> if else
	- pattern endurskilgreiningar basically
		- must be exhaustive

Map í sml
- beitir falli f á sérhvert stak í lista x
- fun map f\[] = \[]
- | map f (a::y) = (f a):: map(f y)

Nafnlaus föll sml
- (eins go lambda segðir)
- fn formal parameters => body

tilgreind tög (explicit types)
- fun add(x,y): real = x + y -> tekur inn og skilar real
- oftast óþarfi

Fjölvirk föll
- hægt að kalla á með viðföngum af fleiri en einu tagi

að binda nöfn við gildi
- gert með let
	- let val newName = expression in expression2 (which includes expression) end;

Exception handling í ML (frábrigði)
- skilgreint með 
	- exception Nomatch
	- raise exceptionName
- Að bregðast við frábrigðum
	- expression handle exceptionName => expression2

Unit í ML
- grunntag í ML (eins og void í C, nema að unit hefur gildið "()" )
- kemur fyrir sem leppur í falli sem lítur út fyrir að taka 0 viðföng
	- fun hello() = "hello world" -> eitt viðfang
- listi af segðum sem skilar gildi síðustu segðarinnar
	- (firstExpression; ...; lastExpression);

Structure í ML
- safn af tögum, föllum, frábrigðum og fleira sem við viljum hjúpa (encapsulate)
	- open Int -> sjá hvað er skilgreint í structure


Curried functions í ML
- Föll fun (x, y) -> fall sem tekur eitt viðfang
- ekki með svigum er curried form
- Hægt að búa til ný föll sem beitt er á sum en ekki öll viðföng upphaflega curried fallsins
- Sérhvert fall með n viðföngum er hægt að breyta í fall með (n- 1) viðföngum os.frv. endurkvæmt þar til öll viðföng hafa verið fjarlægð
- Úr verður partially instantiated function


Samsetning falla í ML (function composition)
- t.d. G og F sem verður nýtt fall C, þannig að fyrir sérhvert viðfang X er 
	- C(x) = G(F(X))
	- G o F -> G bolla F -> samsetning fallanna G og F (G(F(X)))
- Föll geta bæði tekið inn og skilað föllum




![Screenshot 2024-04-23 at 14.11.19.png](../images/Screenshot%202024-04-23%20at%2014.11.19.png)


LISP -> list processor
- Fyrsta forritunarmál til að bjóða upp á 
	- endurkvæmni
	- föll sem fyrsta flokks þegar
	- ruslasöfnun
- Tög
	- Atom
		- Symbol (birtist í formi nafna)
		- númerískir fastar eru líka symbol
	- Listar
		- Skilgreindir sem stök innan sviga
		- Geta innihaldið atom eða aðra lista
- Lambda calculus
- Universal functions sem geta ákvarðað gildi sérhvers annars falls
	- EVAL -> túlkurinn í raun
	- Kviklegar gildissviðsreglur notaðar í fyrstu


Scheme
- LISP mállýska
	- einföld málskipan og merking
- Kyrrlegar gildissviðsreglur
- Föll eru fyrsta flokks þegnar
- EVAL túlkurinn
	- Beitt á grunnfall þá ákvarðar EVAL fyrst gildi viðfanga (með call-by-value)
		- viðföng gætu t.d. verið önnur föll
	- Þegar viðfang er atóm eða listi þá ætti EVAL ekki að ákvarða gildi þess
		- Quote til að segja EVAL að eitthvað sé atom
- Grunnaðgerðir á listum
	- car -> skilar haus (einu staki)
	- cdr -> skilar hala (listanum)
	- cons -> smíðar lista
		- (cons 'a ' ()) -> (a)
		- (cons 'a '(b c)) -> (a b c)
		- tekur frá minni fyrir nýjan lista og skilar til baka bendi á fyrstu sellu hans
	- list -> stytt útgáfa af hreiðruðum cons
		- (list 'a 'b 'c 'd) == (cons 'a (cons 'b ... '() )))
- predicates fyrir boolean
	- eq? number?, symbol?, list?, null?
	- = <> > < >= <= even? odd? zero?
- Listi
	- bara bendir á fyrsta stakið
- Define
	- binda symbol við gildi -> eða binda lambda segðir við nöfn
	- (define mypi 3.14159) (fasti!)
	- (define (functionName parameters) body)
- if then else -> else if líka hægt

SKOÐA cond

Föll sem fyrsta flokks þegnar
- Geta verið útkoma úr gildi segða
- geta verið stök í listum
- hægt að tengja við nöfn
- hægt að senda sem viðföng

let í scheme
- (let ((x1 E1) (x2 E2) ... (xk Ek)) F)
	- gildi allra segðanna E1..Ek er ákvarðað áður en gildin eru bundin við X1...Xk
	- síðan er gildi F ákvarðað með Xi = gildið á Ei
- (+ (suare 3) (square 4))
	- == (let (( three-sq (square 3))
	-            (four-sq (square 4)) )
	- (+ three-squ four-sq) )

Map í scheme
- map squrea '(3 4 2 6)' -> beitir square á car fyrir sérhvert stak

Föll sem búa til þulu
- hægt að kalla á EVAL í falli og þannig hægt að búa til fall í falli og síðan strax ákvarða gildi þess eval(cons '+ lis) (scheme-report environment 5) 

Kyrrlegar vs kviklegar gildissviðsreglur í scheme
- 


![Screenshot 2024-04-23 at 14.47.52.png](../images/Screenshot%202024-04-23%20at%2014.47.52.png)



Hefðbundin forritunarmál
- Gildisveiting eitt helsta einkenni (breytir gildi breytu)
	- hægt að byggja útreikinga á breytingum á stöðu
- hjartað í þeirri aðferð er hugmyndin um modifiable variable
	- Nafn sem við útreikninga er hægt að gefa mismunandi gildi
	- tengsl nafns við minnissvæði stýrist af umhverfinu
- Gildisveitingin breytir ekki tengslum breytunafnsins og minnissvæðisins sem það stendur fyrir


Von Neumann machine
- Reikningar / skipanir snúast um að breyta gildum í minnissvæðum
- forritunarmál eru útdráttur af undirliggjandi hefðbundnum vélbúnaði
- (útreikningar með stöðu)

Útreikningar án stöðu  -> fallaforritunarmál
- útreikningar byggja á að endurskrifa segðir
	- Breytingar sem gerast í umhverfinu en tengjast ekki hugmyndinni um minni
	- breyta umhverfinu þar sem æðri föll eru megin tólin
- útreikningar án breytna eða stöðu (engar gildisveitingar)
- Endurkvæmni kemur í stað ítrunnar
	- ítrun hefur enga merkingu
	- Lykkja breytir stöðu á endurtekinn hátt þangað til gildi tiltekinnar breytu uppfyllir eitthvað skilyrði
- No side effects
	- Eliminates a major source of bugs, and makes the order of exeuction irrelevant
	- no need to describe flow of control
- Föll geta verið expressible gildi 
	- niðurstaðan úr útreikningi á flóknum segðum

Imperative programming -> gildingarforritun


Lambda calculus
- Hugrænt líkan til að lýsa reiknanlegum föllum
- Lisp o.fl. innblásin af lambda calculus

Fallaskilgreining í ML ::  val f = fn x => x * x; 

(fn y => y + 1) (6) -> kall á nafnlaust fall með viðfanginu 6


Fallasegðir
- skila nafnlausu falli sem tekur eina færibreytu y og skilar x + y

Útreikningur með styttingu (reduction)
- ferlið að breyta flókinni segð yfir í gildi hennar (evaluation)
- ferlið kallast stytting (reduction)
- í flókinni segð, er hlutsegð á forminu "function applied to an argument" skipt út með texta fallsins þar sem leppnum er jafnframt skipt út fyrir viðfangið

Grundvallaratriði fallaforritunarmála
- abstraction
- application
- einsleitni
	- Föll er hægt að senda sem viðföng í önnur föll
	- föllum er hægt að skila sem niðurstöðu úr öðrum föllum
		- æðri föll
		- föll eru fyrsta flokks þegar
	- einsleitni milli forrita og gagna

First-class functions
- functions that can be treated as any other data type

Merkingafræðilegt sjónarhorn
- Forrit samanstendur af röð af skilgreiningum
- sérhver skilgreining býr til ný tengsl í umhverfinu og getur haft í för með sér að reikna þurfi út úr flóknum segðum
- Tilvist æðri falla og endurkvæmni gerri þessa forritunaraðferð sveigjanlega og kraftmikla

æðri fall
- fall sem tekur eitt eða fleiri föll sem viðföng

Redex og Reductum
- Redex (reducible expression)
	- ((fn x => body) arg)
- Reductum of a redex er segð sem fæst með því að skipta út sérhverju tilviki af leppnum x í body fyrir afrit af viðfanginu arg
- beta-rule (beta reduction): replacing the redex by its reductum
	- basically að afar í gegn og reikna reductum fyrir sérvhert redex, og skipta því út

Gildisákvörðun
- G = fn x => ((fn y => y + 1) 2);
	- fn x = 2 -> er gildisákvörðun
- Leftmost evaluation order (vinstri gildisákvörðun) er algeng (innermost eða outermost)
- Fer ekki fram við skilgreiningu á föllum
- Leiðir
	- Evaluation by value
		- Applicative order (eager / innermost)
		- gildið á redex er eingöngu ákvarðað ef viðfangið er þegar gildi
			- ![Screenshot 2024-04-23 at 15.28.30.png](../images/Screenshot%202024-04-23%20at%2015.28.30.png)
	- evaluation by name
		- Delayed evaluation, normal order, outermost
		- gildi redex er ákvarðað áður en gildi viðfangsins er ákvarðað
			- ![Screenshot 2024-04-23 at 15.31.04.png](../images/Screenshot%202024-04-23%20at%2015.31.04.png)
		- 
	- lazy evaluation
		- variation of evaluation by name
			- í eval by name gætir þurft að ákvarða gildið á tilteknu redex oftar en einu sinni
			- gildi redex er vistað og sótt síðan ef sama redex kemur upp aftur seinna í ferlinu

Lambda calculus
- Introduces the idea of functions as arguments
- Lambda abstraction
	- (Lx. ((+1) x)); can be simplified to (Lx. + 1 x)
		- equivalent to (lambda (x) (+ 1 x)) in scheme
		- A nameless fucntion which accepts x and adds one to it
- Parentheses are needed for function application to eliminate ambiguity
- The basic operation of lambda calculus is the application of functions
	- beta conversion
- A variable x in an expression (Lx. E) is said to be bound by Lambda
	- The scope of the binding is the expression E
	- An unbound variable is said to be free
- Pass by value or pass by name
	- Pass by value
		- reikna fyrst, síðan senda inn í fuction
	- pass by name
		- delayed evaluation, outermost evaluation, normal order
		- senda inn í function, reikna síðar

Currying
- any function which takes n arguments can be converted to a function with n-1 arguments and so on until all n arguments have been removed
![Screenshot 2024-04-23 at 16.12.27.png](../images/Screenshot%202024-04-23%20at%2016.12.27.png)


Smalltalk
- a pure object-oriented langauge
	- Everything is an object
		- Uniform and elegant
	- Objects have their own memory
	- Class holds the shared behavior for its instances
	- Classes are organized into a singly-rooted tree structure called the inheritance hierarchy
	- Object communicate by sending and receiving
	- Designed bottom up with OO in mind
- Messages
	- can be parameterized with variables that reference objects
	- can return objects
	- All objects are allocated in heap
		- referenced through variables
		- implicit de-referencing
		- automatic garbage collection
	- Dynamic binding (polymorphism)
		- when message sent to object, a corresponding method is searched for
		- else search in superclass, up the tree
		- if never found -> error
		- Search is dynamic Messages are not bound statically
	- Smalltalk variables
		- typeless (any name can be bound to any object)
		- only one type error possible (when a message is sent to an object that has no matching method) -> detected at run-time
	- Supports only single inheritance
- Interpreted language

The smalltalk environment
- Smalltalk (the language) is part of the environment
- An environment where you write your programs
	- 1st GUI design studio
	- editor, translator, virutal machine
	- Environment is written in SmallTalk (can be modified by user)


Hugræn gagnatög (abstract data type)
- Tryggja húpun og upplýsingahuld á gögnum og aðgerðum á skilvirkan hátt
	- sameina í eina heild bæði gögn og aðgerðir til að meðhöndla þau
	- þau geta komið í veg fyrir að tilteknir þættir hugbúnaðarhluta séu aðgengilegir notendum
- Vandamál
	- Ósveigjanleiki
		- Kemur fram þegar til stendur að bæta við eða endurnýta hugrænt gagnatag
	- Samræming
		- Að meðhöndla á samræmndan hátt gildin á datatype1 og datatype2 sem útfæra sama eða svipað viðmót
			- til dæmis geyma fylki sem getur geymt bæði gagnatög
			- Ekki hægt í hugrænum gagnatögum því föll þeirra eru fjölbundin á kyrrlegan hátt
			- þannig að fylki af gagnatagi 1 myndi alltaf nota samsvarandi fall skilgreint í gagnatagi 1
		- Lausn -> concept of compatibility

Samhæfing
- T er samhæft við S þegar allar aðgerðir á gildum af taginu S eru líka mögulegar á gildum á taginu T


Hlutbundin mál
- megin einkenni
	- Útdráttur (hjúpun og upplýsingahuld)
	- undirtög (subtypes) (samhæfni)
	- erfðir (inheritance)
	- kvikleg binding (dynamic binding)
- Klasi
	- Klasi er tæki til að framkvæma útdrátt
	- hjúpar gögn og aðgerðir á þeim
	- býður upp á skil (interface)
	- sérhver hutur tilheyrir a.m.k. einum klasa
	- skilgreinir breytur og aðgerðir sem gerir tilvikum klasans kleift að haf astöðu (state) og hegðun (behavior)
	- Einfaldasta útfærslan notar tengdan lista fyrir klasastigveldið
		- Sérhver hnútur stendur fyrir klasa og inniheldur bendi á útfærslur á aðgerðum í klösunum.
		- Hnútarnir eru tengdir saman með bendum sem benda frá undirklasa til yfirklasa
		- þegar boð m eru send til tilviks o af klasa C þá er bendir, sem geymdur er ´io, notaður til að nálgast c og ákvarða hovrt C inniheldur útfærslu á m
		- ef ekki, þá er leiðta í yfirklasanum o.s.frv.
		- Þessi aðferð er notuð í Smalltalk þrátt fyrir að hún sé óskilvirk því við sérhver boð þarf að leita línulega að réttu útfræslunni í klasastigveldinu
	- Stöff
		- Meðlimaföll
			- aðgerðir sem meðhöndla hluti (member functions)
			- Hafa aðgang að tilvikabreytum
			- keyrð með því að senda boð til hlutar
				- Kviklegt val velur rétt fall til að keyra
		- tilvikabreytur
			- eigindi hvers tilviks
		- Boð (message)
			- fallaköll (essentially)
- Hlutur
	- tilvik af klasa
	- færsla (struct / record)
	- sum siðv færslunnar standa fyrir gögn
	- önnur svið færslunnar standa fyrir aðgerðir til að meðhöndla gögnin
	- Hægt að setja fram sem færslu með eitt svið fyrir sérhverja tilvikabreytu sem skilgreind er í viðkomandi klasa, til viðbótar við breyturnar sem skilgreindar eru í yfirklasanum.
	- Framsetning hlutarins inniheldur einnig bendi á klasann sem hluturinn er tilvik af


Útfærsluatriði
- tilvikaaðgerð er keyrð á svipaðan hátt og föll
- kvaðningafærsla með staðværu breytum, leppum og öllum öðrum upplýsingum er sett á staflann
- ólíkt föllum þá þarf tilvikaaðgerð að haf aðgnag að tilvikabreytunum.
- Hvaða tag nákvæmlega um ræðir er ekki þekkt á þýðandatíma
- Strúktúr tilviksins er þekktur (enda háður klasanum) og því er offset sérhverrar tilvikabreytu þekkt á þýðandatíma.
- Bendir á tilvikið semfékk boððin er sendur sem viðfang þegar kallað er á viðkomandi fall
- this í c++ og self í Python
- Þegar fallið er keyrt þá er vísað í tilvikabreytu með offset frá þessum bendi
	- í stað þess að hafa offset frá kvaðninafærslubendi eins og þegar um staðværar breytur falls er að ræða
- KYRRLEG tögun : skilvirkari útfærsla
	- að velja réttu útfærsluna á aðgerð tekur fastan (constant) tíma
	- Ef tög eru kyrrleg þá eru mengi aðgerða sem hægt er að keyra fyrir tiltekinn hlut, þekkt á þýðandatíma
	- Listi af þessum aðgerðum er geymdir í klasanum sjálfum (class descriptor)
	- Listinn inniheldur ekki einungis aðgerðis sem eru skilgreindar í klasanum heldur einnig allar aðgerðir sem klasinn erfir frá yfirklasa
	- í C++ er notað hugtakið vtable (virtual function table) fyrir þessa gagnaskipan
	- Ef Sérhver klasi hefur eigin vtable
	- öll tilvik af sama klasa deila sömu vtable
	- þegar undirklasi B af A er skilgreindur, þá er vtable fyrir B búin til með því að afrita vtable fyrir A, öllum aðgerðum sem eru endurskilgreindar í B skipt út og nýjum aðgerðum í B bætt við
	- ![Screenshot 2024-04-23 at 20.29.29.png](../images/Screenshot%202024-04-23%20at%2020.29.29.png)
		- ef B er undirklasi A þá er fyrsti hluti vtable fyrir B afrit af töflunni fyrir A
		- að kalla á tilvikaaðgerð kostar aðeins það að fylgja tveimur bendum
			- offset sérhverrar aðgerðar í vtable er þekkt á þýðandatíma


Hlutur vs. ADT
- Þegar ADT breyta er skilgreind þá stendur hún aðeins fyrir þau gögn sem hægt er að meðhöndla með aðgerðum
- Sérhvert tilvik af klasa er gámur sem raunverulega hjúpar bæði gögn og aðgerðir

Kóði meðlimafalla
- aðeins eitt afrit af kóða meðlimafalla er tengdur við klasann
- þegar tilvik af klasa þarf að keyra tiltekið meðlimafall þá er kóða fallsins flett upp í klasanum
- Tilvikabreytur eru geymdar í sérhverju tilviki
- Hluturinn sem fær boðið er einnig óbeint viðfang

Klasabreytur og klasaaðgerðir (static variables and methods)
- Tengja breytur og aðgerðir við klasann frekar en tilvik
- klasabreytur eru geymdar í klasanum með meðlimaföllunum
- Geta ekki vísað í this, hafa ekki aðgang að neinu tilviki

Undirtög / hluttög
- Tag sem tengist klasanum T er undirtag (subtype) klasans S ef sérhvert boð sem hlutur af S skilur er einnig skilið af hlutum af taginu T
	- T er undirtag S þegar skil (interface) S er hlutmengi af skilum T
- Ef hlutur er settur fram sem færsla (e. record) sem inniheldur gögn og föll, þá er T færslutag sem inniheldur öll svið úr S og hugsanlega önnur svið


Undirklasi (subclass) (yfirskrift)
- megin einkenni undirklasa er möguleikinn á að breyta skilgreiningu (útfærslu) á aðgerð sem skilgreind er í yfirklasa
	- yfirskrift (overriding)

Erfðir
- Þegar undirklasi yfirskrifar ekki aðgerð þá erfir hann hana af yfirklasanum.
- Útfærslan á aðgerðinni í yfirklasanum er aðgengileg undirklasanum
- erfðir gera kleift að skilgreina nýja klasa með því að endurnýta klasa sem þegar eru til.

Munur á erfðum og undirtögum
- Undirtag : geta notað hlut í öðru samphengi, samband milli skila í tveimur tögum (compatibility of interfaces)
- Erfðir : geta endurnýtt kóða sem meðhöndlar hlut. Samband á milli útfærslu tveggja klasa
- í flestum hlutbundnum málum (OOL) ef T er undirklasi S þá er T jafnframt undirtag S

í C++
- ef yfirklasinn er ekki public þá er um erfðir að ræða en ekki undirtagasamband.

Kvikleg binding (dynamic binding)
- Eitt mikilvægasta atriðið í hlutbundnum málum
- Tryggir að kallað verður á réttu aðgerðina í hvaða teljara sem er
- Þýðandinn getur ekki ákvarðað hvert tagið verðu á hlut (verður ekki ljóst fyrr en á keyrslutíma) og þess vegna þarf þessi binding að vera kvikleg
- Þegar boð m er sent til hlutar o þá geta verið margar mögulegar útgáfur af útfærslu á m fyrir o
- Val á útfærslu fyrir m er háð taginu á hlutnum sem fær boðin.


High level language
- Skipan og aðferðir til að skipuleggja gögn
	- Byggja á tagkerfi (type system) málsins
- Tög eru eitt af mikilvægustu eiginleikum forritunarmála og það sem aðgreinir eitt mál verulega frá öðru

Gagnatag
- einsleitt (homogenous) safn gilda með skilvirka skipan (effectively presented), búið mengi aðgerða til að meðhöndla þessi gildi
- ástæður fyrir tilvist gagnataga
	- á hönnunarstigi
		- stuðningur við hönnun / skipulagið (conceptual organization)
		- Gerir hönnuði kleift að nota það tag sem hentar hverjum flokki hugtaka best
		- Mismunandi hugtökum má lýsa með mismunandi tögum, með eigin mengi af aðgerðum.
		- Notkun mismunandi taga sem bæði hönnunar- og skjalatól
	- á forritunarstigi
		- sem stuðningur við réttleika (correctness)
		- Sérhvert forritunarmál á sér sitt eigið mengi af reglum fyrir tagskoðun (type checking)
		- Þess konar skilyrði á tögum geta bæði komið í veg fyrir keyrsluvillur og lógískar (merkingalegar) villur
	- á þýðingarstigi
		- sem stuðningur við útfærslu (implementation)


Tagskoðari (type checker)
- ákvarðar hvort tagskilyrðum (type constraints) sé fullnægt fyrir keyrslu (og fyrir myndun þulu; code generation) forrits
- hluti af þeim fasa þýðanda sem sér um að skoða setningafræðileg skilyrði háð samhengi (contextual syntactic checking)

tög -> controlled comments
- Tög gefa til kynna hvernig forritari hugði sér að hlutir gætu verið notaðir (á löglegan hátt)
- (ólíkt athugasemdum þá) finnur þýðandinn (eða sýndarvélin) ranga notkun á þessum hlutum

Tög geta verið takmarkandi (restrictive)
- t.d. að þurfa að skilgreina mismunandi fall til að sortera lista af mismunandi tögum -> lausn t.d. templates í c++

Tög
- Tög eru mikilvægar upplýsingar fyrir sýndarvélina
	- t.d. stærð minnis
- kyrrleg tögun
	- þegar tög eru til staðar þá eru þessar upplýsingar aðgengilegar á kyrrlegum tíma og breytast ekki á meðan á keyrslu stendur
	- kyrrleg úthlutun við þýðingu -> mögulegt að besta aðgerðir sem vísa í hlut
	- aðgangur að breytu í kvaðningafærslu er útfærð með offset frá bendi á kvaðningafærslu

Tagkerfi (type system)
- mengi af fyrirfram skilgreindum tögum í málinu
- Aðferðum við að skilgreina ný tög
- aðferðum við að stýra tögum:
	- jafngildisreglur (equivalence rules) 
		- segja til um hvenær tvö formlega mismunandi tög samsvara sama taginu
	- Samhæfisreglur (compatibility rules)
		- segja til um hvenær gildi eins tags getur verið notað í samhengi þar sem annars tags er krafist
	- reglur og aðferðir við tagályktun (type inference)
		- segaj til um hvernig málið úthlutar tagi til flókinnar segðar byggt á upplýsingum um einstaka hluta hennar
- upplýsingar um hvort tagskoðun er kyrrleg eða kvikleg


Stragnlega tagað mál (strongly typed language)
- Type safe language
- Þegar ekkert forrit getur í keyrslu framkallað unsignalled villu sem má rekja til tagvillu
	- type casting í "vitlaust gildi" er dæmi um tagvillu á keyrslutíma (c++ er þar með ekki stranglega tagað)

Kyrrleg tagskoðun
- ef hægt er að framkvæma tagskoðun á þýðandatíma
- kostir
	- Villur tilkynntar um leið og forritið er þýtt
		- minnkar prófanir og aflúsun
	- utanumhald um tög á keyrslutíma er óþarft vegna þess að réttleiki er tryggður við þýðingu
	- keyrsla forrits er skilvirkari - tagskoðun fer ekki fram við keyrslu
	- Betri skjölun í formi kyrrlegra taga
- Ókostir
	- hönnun kyrrlega tagaðra mála er flóknari en kviklegra tagaðra, sérstaklega ef type safety á líka að vera tryggt
	- Þýðing er flóknari og tekur lengri tíma
		- Samt lítill kostnaður vs. að finna villur á keyrslutíma


Kvikleg tagskoðun
- tagskoðun fer fram á keyrslutíma
- g.r.f. að sérhver hlutur / gildi hafi run-time-descriptor sem tilgreinir tag þess
- möguleg með því að láta þýðandann búa til viðeigandi tagskoðunarkóða, eða forrita tagskoðunarkóða í túlki, sem er keyrður á undan sérhverri aðgerð
- Kostir
	- Sveigjanleiki fyrir forritarann
	- Fljótari þróunartími 
	- betri tjáningarhæfni
- ókostir
	- hægari keyrsla (overhead) (vegna tagskoðunar á keyrslutíma)
	- Villa kemur ekki fram fyrr en á keyrslutíma þegar endanotandinn er að nota forritið / kerfið

Kyrrlega töguð - C / C++, Java
Kviklega töguð - Python, Ruby, Perl


Gagnaútdráttur (data abstraction)
- Flest forritunarmál hafa 
	- fyrirfram skilgreind tög
	- leiðir til að skilgreina ný tög (samsett tög)
		- Oft takmarkað
			- finite homogenous aggregations (arrays)
			- heterogenous ones (records)
			- aðgerðir oft fyrirfram skilgreindar af málinu 

Hugræn gagnatög
- hjúpar gögn og aðgerðir á þeim
- fyrirfram skilgreindur gagnaútdráttur (tög) þar sem útfærslan er falin en forritarinn getur ekki skilgreint þess konar tög sjálfur
- Önnur mál (t.d. OO) leyfa skilgreiningar á gagnaútdrátti sem haga sér eins og grunntög í skilningi þess að útfærslan er falin
- Einkenni
	- Nafn fyrir tagið
	- útfærsla (framsetning) á taginu
	- mengi af aðgerðum til að vinna með gildi tagsins
	- útfærsla á sérhverri aðgerð sem byggir á framsetningunni
	- leið til að aðskilja nafnið á taginu og nöfn aðgerða frá útfærslunni
- Skil (interface)
	- Nafn tagsins og tög aðgerðanna eru sýnileg utan frá
- ósýnilegt utan frá
	- útfærsla tags og aðgerða
	- Upplýsingahuld (information hiding)
		- Fall felur útfærslu en opinberar skilin (nafn falls, fjölda og tög leppa)
		- Gagnaútdráttur tekur þetta frumstæða útdráttarform lengra
			- útfærsla aðgerðar og framsetning gagnanna falin

Hjúpun
- það að setja saman gögn og aðgerðir sem vinna á þeim

Upplýsingahuld
- það að koma í veg fyrir að hluti hugbúnaðar (útfærsla) sé aðgengilegur notendum

Hugrænt gagnatag
- gagnatag sem skilgreint er með tilliti til aðgerða á því og útfærsla þess er falin

útdráttur (to abstract)
- að fela eitthvað
- Forritunarmál er útdráttur af tölvu

Abstraction mechanisms
- ferlaútdráttur
	- gerir kleift að fela nákvæma virkni tiltekins ferlis (falls)
- gagnaútdráttur
	- gerir kleift að nota gagnatög án þess að vísa í vhernig tögin eru útfærð

Niðurbrot (decomposition á vandamáli)
- brjóta vandamál niður í smærri, meðfærilegri einingar.

Undirforrit (subprograms)
- lykilhugtak sem öll nútíma forritunarmál bjóða upp á

Fall
- kóðabútur auðkenndur með nafni
- fær eigið staðvært umvherfi (local environment)
- Skiptir á upplýsingum við annan hluta forritskóðans í gegnum 
	- stika (parameters)
	- skilagildi (return value)
	- umhverfi sem er ekki staðvært (non-local environment)
- Málfræðilegur stuðningur
	- skilgreining (definition) eða yfirlýsing (declaration) á falli
	- notkun falls (fallakall)

Stikar (parameters)
- leppar (formal parameters)
	- koma fyrir í skilgreiningu á falli
	- haga sér eins og staðværar skilgreiningar
- Viðföng (actual parameters)
	- koma fyrir í kallinu sjálfur


Skilagildi
- Föll koma upplýsingum til skila til annarra hluta forrits með því að skila gildi sem stendur fyrir niðurstöðu fallsins.
- Í sumum forritunarmálum er nafnið "function" frátekið fyrir undirforrit sem skilar gildi
- Í forritunarmálum sem byggja á C eru öll undirforrit föll
	- ef skilatags falls er void, þá skilar fallið ekki þýðingarmiklu gildi

Procedure
- undirforrit sem hefur samskipti við caller eingöngu í gegnum stika eða nonlocal umvherfi
- s.s. ekkert skilagildi

non-local umhverfi
- fall getur skipst á upplýsingum við aðra hluta forrits með því að nota breytur sem skilgreindar eru í non-local umhverfinu
- ef kóði fallsins breytir gildi non-local breytu, þá hefur það áhrif á aðra hluta forrits þar sem breytan er sýnileg


Stikun færibreytna (parameter passing)

Aðferð við stikun færibreytna
- para viðföng (actual parameters) við leppa (formal parameters) og merkingin sem tengist því

Tegundir færibreytna
- inntaks færibreyta (input parameter)
- úttaksfæribreyta (output parameter)
- inntaks/úttaksfæribreyta (input/output parameter)

l-value 
- gildi sem stendur fyrir minnissvæði og kemur þess vegna fyrir á vinstri hlið gildisveitingar

r-value
- gildi sem hægt er að geyma í minnissvæði og er þess vegna gildi segðar sem kemur fyrir á hægri hlið gildisveitingar

Aðferðir við stikun færibreytna (parameter passing mode)
- Call by value
	- inntaksfæribreyta
	- Staðværa umhverfi fallsins er útvíkkað með leppnum 
	- Viðfangið sjálft getur verið segð
	- r-value viðfangsins er tengt við leppinn (ekki l-value)
	- það er engin leið að nota call-by-value til að senda upplýsingar frá callee í caller
	- kóperað
	- Leppurinn á sér minnissvæði í kvaðninafærslu callee
		- Gildi viðfangsins er sett í þetta svæði á calling sequence af caller
	- Kostðanarsöm aðgerð þegar viðfangið er stór gagnaskipan -> gögn afrituð yfir í leppinn
	- Sjálfgefin aðferð við stikun færibreytna í mörgum forritunarmálum og eina ðaferðin t.d. í C og Java
- Call by reference
	- Útfærsla á aðferð þar sem færibreyta getur verið notuð fyrir bæði inntak og úttak
	- viðfangið verður að vera segð með l-value
	- tengsl mynduð milli leppsing og l-value viðfangsins sem býr til aliasing
	- sérhver breyting á leppnum er breyting á viðfanginu
	- Leppurinn á sér minnissvæði í kvaðningafærslu fallsins
		- l-value viðfangsins (bendir) er geymt í þessu minnissvæið þegar calling sequence er framkvæmt
	- hraðvirk aðgerð, þarf eingöngu að geyma bendi (engar afritanir)
- Call by result (andstæðan við call by value)
	- output-only aðferð
	- viðfangið verður að vera segð með l-value
	- þegar fallið hættir keyrslu þá er núverandi gildi leppsins afritað yfir í l-value viðfangsins
	- engin leið að nota result færibreytu til að koma upplýsingum frá caller til callee
- Call by value-result
	- samsetning (combination) call by value og call by result -> bidirectional communication
	- viðfangið þarf að vera segð með l-value
	- í byrjun fallsins er r-value viðfangsins afritað yfir í leppinn
	- í lokin er núverandi gildi leppsins afritað yfir í l-value viðfangsins

Java object reference
- Java hefur ekki bendi
- Aka þegar maður setur hlut sem inntaksfæribreytu í fallakall.

Æðri föll
- higher order ef það getur tekið við föllum í gegnum leppa eða skilað öðru falli sem niðurstöðu
- föll sem færibreytur
- föll sem skilagildi

Tegundir bindinga
- tveir möguleikar til að velja non-local umhverfi þegar kallað er á fall f sem er með lepp (fall) h
	- Deep binding
		- Nota umhverfið sem er virkt á þeim tíma þegar tenging milli h og f er búin til 
		- Öll tungumál sem nota kyrrlegt gildissvið nota líka deep binding
		- Kyrrlegur bendir ákvarðaður á þeim tímapunkti sem tengslin milli leppsins og viðfangsins eru mynduð (viðfangið er fall)
		- leppurinn h þarf ekki eingöngu að tengja við kóðann fyrir f heldur líka non-local umvherfið sem nota á við keyrslu á f
		- í blokkinni þar sem kallig g(f) á sér stað, getum við á kyrrlegan hátt tengt nestin level á skilgreiningunni á f við viðfangið f
		- leppurinn er því tengdur við par (bendir á kóða, bendir á kvaðninafræslu) sem kallað er closure
		- fyrri hluti parsins er notaður til að færa flæði forritsins í rétt fall og seinni hluti parsins notaður til að gefa kyrrlega hlekknum í nýju kvaðninafærslunni það gildi
	- Shallow binding
		- Nota umhverfið sem er virkt þegar kallið í f með h sem viðfang á sér stað
	- Skoða 404
- combinationir
	- Deep binding og kyrrlegt gildissvið
	- Deep binding og kviklegt gildissvip
	- shallow binding og kyrrlegt gildissvið



Föll sem skilagildi
- að skila falli sem gildi úr öðru falli gerir kleift að búa til föll á kviklegan hátt á keyrslutíma
	- Fall sem skilað er sem gildi, þarf að vera táknað á keyrslutíma með kóða þess og umhverfinu sem notað verður við keyrslu þess
	- þegar fall skilar falli þa´er gildið sem sagt closure
	- kyrrlegi hlekkur fallins sem er skilað er þá ákvarðaður með því að nota seinni hlutann í viðkomandi closure
- Vandamál
	- hægt að skila falli sem er skilgreint inni í hreiðraðri blokk og vísar í nafn sem er í kvaðningafærslu sem verður eytt
		- lausn: ekki nota stafla fyrir kvaðningafærslur til að þær geti lifað áfram eftir að viðkomandi fall hættir keyrslu
		- í fallaforritunarmálum er kvaðningafærslum úthlutað minni á hrúgunni


Minnismeðhöndlun
- eitt af hlutverkum túlks sem tengist sýndarvél
- stýrir úthlutun minnis fyrir forrit og gögn

low level sýndarvél vs. high level sýndarvél
- í tilviki vélarmáls er minnismeðhöndlun einföld og getur verið alfarið kyrrleg
- í tilviki high leve forritunarmáls er allt flóknara
	- ef málið leyfir endurkvæmni þár er kyurrleg úthlutun ekki nægjanleg. Fjöldi samtímis virkra fallakalla fer eftir gildum viðfanga sem send eru inn í fallið

Endurkvæmni
- sérhvert fallakall þarf á eigin minnissvæði að halda til að gyema
	- viðföng 
	- milliniðurstöður (intermediate results)
	- afutrhvarfsvistfang (return address)
	- ofl
- Kyrrleg úthlutun minnis er ekki nægjanleg
- Kvikleg úthlutun minnis og deallocation eru nauðsynleg á keyrslutíma
	- Hægt að útfæra með keyrslustafla
	- Heap er notað þegar setning í forriti biður um úthlutun á kviklegu minni

Kyrrleg minnismeðhöndlun
- Einkenni
	- framkvæmd af þýðandanum áður en keyrsla forrits hefst
	- hlutir, sem úthlutað er kyrrlegu minni eru geymdir í fyrirfram skilgreindu svæði í minni og eru þar á meðan forritið keyrir
		- víðværar breytur (global variables)
		- vélarmálskóði
		- töflur sem þýðandinn býr til (nafnatafla)
- Ef forritunarmál leyfir EKKI endurkvæmni þá er hægt að úthluta minni fyrir staðværar breytur falls á kyrrlegan hátt

Kvikleg minnismeðhöndlun með stafla
- Komið er inn og út úr blokkum með LIFO (last in first out)
	- þegar komið er inn í blokk A og þaðan í blokk B, þá er nauðsynlegt að fara fyrst út úr blokk B áður en farið er út úr blokk A
- Stafli er notaður til að halda utan um minni sem er staðvræt í sérhverri blokk

Kvaðningafærsla (activation record)
- minnissvæið á keyrslustaflanum sem tilheyrir "in-line" blokk eða kvaðningu (activation) falls
- tengist sérstakri kvaðningu falls og er búin til þegar kallað er á fallið


Keyrslustafli
- stafli sem geymir kvaðningafærslur (á keyrslutíma)


Kvaðningafærslur fyrir in-line blokkir
- milliniðurstöður
- staðværar breytur
	- þarf að geyma í minnissvæði. Stærð er háð fjölda og tagi breytna
	- upplýsingar teknar af þúðandanum sem getur ákvarðað stæðina á þessum hluta kvaðningafærslunnar
- kviklegur bendir (dynamic chain pointer)
	- bendir á kvaðningafærsluna sem er næst á undan á staflanum
	- Nauðsynlegt því almennt getur stærð kvaðningafærslna verið mismunandi.

Kvaðningafærslur fyrir föll
- Eins og in-line blokkir nema þarf meira af upplýsingum til a ðstýra keyrsluflæði (control flow)
- Fall sem skilar einnig gildi til þess sem kallar (ef engu gildi er skilað þá procedure)
- Geyma
	- Milliniðurstöður
	- staðværar breytur
	- kviklegur bendir
		- bendir á tiltekið fast svæði (yfirleitt nálægt miðju) í kvaðningafærslunni á undan
		- Vistföng á mismunandi sviðum fengin með því að bæta negatívu eða pósitívu offset við gildið á þessum kviklega bendi
		- þýðandinn skiptir út tilvísunum í staðværar breytur fyrir vistfögng miððað við fasta staðsetningu (offset) í kvaðningafærlsunni
			- Hægt vegna þess að röð yfirlýsinga á breytum er þekkt á þýðandatíma
		- Hægt að nota til að þrufa ekki að framkvæma leit að rétta minnissvæðinu á keyrslustaflanum.
	- kyrrlegur bendir
		- geymir upplýsingar sem nauðsynlegar eru til að útfæra kyrrlegar gildissviðsreglur
	- Afturhvarfsvistfang (return address)
		- geymir vistfangið á fyrstu skipun sem á að keyra eftir að fallið lýkur keyrslu
	- Skilagildi
		- bendir á minnissvæði í kvaðningafærslu þess falls sem kallaði. Fallið sem kallað er á setur skilagildið þar inn
	- Viðföng
		- gildi viðfanga sem notuð er í fallakallinu

Kvaðningafærslur
- settar og fjarlægðar af staflanum á keyrslutíma
	- þegar komið er í blokk / fall -> push
	- þegar farið er út úr blokk / falli -> pop

Caller -> það fall sem kallar
Callee -> falið sem kallað er á

Meðhöndlun staflans
- gerð af bæði caller og callee (skipting fer eftir þýðendum og tiltekinni útfærslu)
- Calling sequence 
	- Kóði (sem þýðandinn setur inn) í caller sem keyra þarf að hluta til áður en kall á sér stað og að hluta til eftir á
- prologoue
	- Kóði sem keyrður er af callee strax eftir að kallið á sér stað
- epilogue
	- Kóði sem keyrður er af callee þegar fallið hættir keyrslu
- ÁÐur en fallið byrjar keyrslu (caling sequence og prologue)
	- breyta program counter
		- til að flæði forritsins fari í callee.
		- Geyma gamla gildi program counter í afturhvarfsvistfangi (+1)
	- úthluta svæði á staflanum
		- uppfæra top-of-stack bendinn
	- breyta activation record pointer
		- Bendir á nýju kvaðningafærsluna sem var verið að setja á staflann
	- stikun færibreytna (parameter passing)
		- framkvæmt af caller
	- gisti
		- upplýsingar í gistum fyrir kall þarf að vista
- Eftir að fall lýkur keyrslu (calling sequence og epilogue)
	- Uppfæra program counter
		- til að flæði fari til baka í callee
	- skilagildi
		- þarf að setja á tiltekinn stað í kvaðningafærslu caller
	- Gisti
		- vistuð gildi á gistum þarf að koma á aftur
	- Deallocation
		- kvaðningafærslu calle þarf að fjarlæga af staflanum með því að breyta top-of-stack pointer

Heap hrúga
- meðhöndla explicit minnisúthlutanir sem geta átt sér stað á hvaða tíma sem er
- svæði í minni þar sem blokkum af minni er hægt að úthluta á tiltölulega frjálsan hátt
- meðhöndlun minnis af hrúgu fellur í tvo megin flokka 
	- föst lengt
	- breytileg lengd


Útfærsla á gildissviðsreglum
- Útfærslan á umvherfi og gildissviði krefst viðeigandi gagnaskipanar
- tilvísun í non-local nafn
	- þarf að skoða kvaðningafærslur sem eru ennþá virkar á staflanum til þess að finna þá réttu sem inniheldur nafnið sem um ræðir
	- Sú kvaðningafærsla samsvarar blokkinni með yfirlýsingu á nafninu (breytunni)
	- í hvaða röð þarf að skoða kvaðningafærslurnar fer eftir því hvers konar gildissvið er um að ræða

Kyrrleg keðja (static chain)
- röð kvaðningafærslnanna sem skoða þarf þegar finna þarf non-local tilvísun fer ekki eftir stöðu þeirra á staflanum
- Kvaðningafærsla sem tengist beint kviklega bendinum er ekki endilega sú fyrsta sem leita þarf í til að leysa non-local tilvísun
- Kyrrlegi hlekkurinn er notaður til að finna færsluna
- Endurspeglar strúktúr á hreiðruðum (nested) blokkum í forritinu
- Framvkæmt af calling sequence, prologue og epilogue
	- þegar farið er inn í nýja blokk / fall þá reiknar caller út kyrrlega bendinn og sendir hann áfram til callee

Útreikningar með kvaðningafærslur
![Screenshot 2024-04-23 at 22.54.00.png](../images/Screenshot%202024-04-23%20at%2022.54.00.png)![Screenshot 2024-04-23 at 22.54.32.png](../images/Screenshot%202024-04-23%20at%2022.54.32.png)

level distance
- reiknanlegt á kyrrlegan hátt
- Gerir mögulegt að finna minnissvæði fyrir non-local tilvísanir ánþ ess að þurfa að leita í kvaðningafærslunum á staflanum

Einfaldari útfærlsa
- kyrrlegan bendi þarf ekki
- Kviklegi bendirinn notaður til að leita að tilvísunum í non-local breytu
- kostnaður er sá að nöfn breytanna þarf að geyma í kvaðningafærslunum (eað í einhverri external gagnaskipan)


Nöfn sem hugræn tæki (abstraction devices)
- Nafn er runa stafa sem notað er til að standa fyrir einvhern annan hlut (object)
- Nöfn leyfa útdrátt (abstraction of )
	- gögnum (nafn til að tákna staðsetningu í minni)
	- stýringu (control) (mengi skipana með nafni)
- tákn geta verið nöfn + og - eru nöfn sem standa fyrir tilteknar grunnaðgerðir
- aliasing
	- þegar einstakur hlutur á fleiri en eitt nafn (í sama umvherfi)
- Tiltekið nafn getur staðið fyrir mismunandi hluti á mismunandi tímum.

Merkjanlegir hlutir (denotable objects)
- hlutir sem hægt er að gefa nafn

Binditími 
- tengsl eða binding nafns og hlutarins sem það stendur fyrir getur orðið til á ýmsum tímum
	- Hönnunartíma máls
	- forritunartíma
	- þýðandatíma
	- keryslutíma

Kyrrlegur -> allt sem á sér stað fyrir keyrslu (það sem gerist á þýðandatíma)
kviklegur -> allt sem gerist á keyrslutíma.

Umhverfi (environment)
- mengi af tengslum milli nafna og merkjanlegra hluta sem er til staðar á keyrslutíma á ákveðnum stað og tíma í forritinu er kallað tilvísunarumhverfi (referencing environment)
- eitt megin einkenni high-level forritunarmála sem herma þarf eftir í sérhverri útfærslu á viðkomandi máli

Yfirlýsing (declaration)
- leið til að kynna til sögunnar tiltekin tengsl í umhverfinu.

Blokkir
- textasvæði í forritinu, merkt með start og end tákni sem getur innihaldið yfirlýsingar sem eru staðværar (local í umræddu svæði)
- tegundir
	- blokk sem tengist falli
		- tengist yfirlýsingu á falli - body fallsins sjálfs að viðbættum yfirlýsingum á leppum (formal parameters)
	- in-line block
		- blokk sem tengist ekki yfirlýsingu á falli og getur kmoið fyrir í hvaða stöðu sem er þar sem skipun getur komið fyrir

Sýnileikaregla
- yfirlýsing sem er staðvær í blokk er sýnileg í þeirri blokk og í öllum blokkum innan hennar, nema að til staðar sé ný yfirlýsing á sama nafni í hreiðruðu (nested) blokkinni. Í því tilviki felur blokkin sem inniheldur endurskilgreiningu nafnsins fyrri yfirlýsinguna.

Tegundir umhverfis
- staðvært (local) umhverfi
	- það mengi af tengslum fyrir nöfn sem eru skilgreind staðvært í blokkinni
	- ef blokkin er fyrir fall, þá inniheldur staðværa umhverfið einnig tengslin fyrir leppana (formal parameters)
- Ekki staðvært umvherfi (non-local)
	- mengi af tengslum fyrir nöfn sem eru sýnileg inni í blokk en sem hefur ekki verið lýst yfir staðvært í blokkinni
- Víðvært (global) umvherfi
	- samanstendur af mengi af tengslum fyrir nöfn sem var lýst yfir þegar forritið hóf keyrslu
	- inniheldur tengsl fyirr nöfn sem hægt er að nota í öllum blokkum í forritinu.
![Screenshot 2024-04-23 at 23.27.42.png](../images/Screenshot%202024-04-23%20at%2023.27.42.png)


Gildissviðsreglur
- kyrrlegar
	- byggt á texta forrits
	- umhverfið sem er í gildi á tilteknum stað í forritinu og á tilteknum stað í keyrslu er eingöngu háð texta forritsins sjálfs
	- getur verið ákvarðað algerlega af þýðandanum
	- skilgreining
		- staðværar yfirlýsingar innan blokkar skilgreina staðvært umhverfi blokkarinnar en yfirlýsingar í hreiðruðum blokkum eru ekki teknar með.
		- Tengsl nafns, sem notað er innan blokkar, er það sem er í gildi í staðvæar umhverfi blokkarinnar. ef engin tengsl fyrir nafn er til í staðværa umvherfinu, þá eru tengsl í umlykjandi (enclosing) blokk athuguð. Þessi leit heldur áfram þangað til komið er í ystu blokkina. Ef engin tengsl finnast þar, og heldur ekki í fyrirfram skilgreindu umhverfi málsins, þá er um villu að ræða
		- Hægt er að gefa blokk nafn (t.d. föll) og í því tilviki er nafnið hluti af staðværa umhverfinu sem inniheldur fallið
	- Kostir
		- sérhvert tilvik af nafni getur verið tengt við rétt yfirlýsingu með því einu að skoða forritskóðann
		- Þýðandinn getur fundið tengslin og því hægt að framkvæma test á þýðandatíma með því að nota upplýsingar um tög nafna
- kviklegar
	- byggt á flæði á keyrslutíma
	- Rétt tengsl fyrir nafn X, á tilteknum stað P í forriti, eru nýjustu tengslin sem búin voru til fyrir X og sem eru ennþá virk þegar flæði forritsins kemur að P
	- kostur
		- sveigjanleiki
	- ókostir
		- erfitt að lesa forritið með tilliti til keyrsluflæðis
		- óskilvirkara í keyrslu samanborið við kyrrlegt gildisvvið


Kyrrlegt vs. kviklegt gildissvið
- Munurinn snýst eingöngu um ákvörðun á umhverfinu sem er hvorki staðvært (local) né víðvært (global) fyrir staðvært og víðvært umhverfi virka reglurnar eins.


Ofansækinn endurkvæmnisþáttari (recursive descent parser)
- safn endurkvæminna undirforrita
- byggir þáttunartré á ofansækinn máta 
- sér undirforrit er skrifað fyrir sérhverja máleiningu í mállýsingunni
	- Byggir þann hluta þáttunartréssins sem byrjar á viðeigandi máleiningu
	- undirforritið er þáttari fyrir mál (mengi af strengjum) sem hægt er að leiða út frá viðkomandi máleiningu.


Þýðendur skipta greiningu málskipan í tvo sjálfstæða hluta
- lesgreining
	- meðhöndlar tóka (litlar máleiningar)
		- nöfn, tölur, virkjar, greinarmekri
- Þáttun
	- meðhöndlar stærri máleiningar
		- segðir, setningar, forritunareiningar
- 
![Screenshot 2024-04-23 at 23.43.14.png](../images/Screenshot%202024-04-23%20at%2023.43.14.png)


Lesgreinir
- leitar að mynstrum í texta
	- reynir að finna hlutstrengi sem passa við ákveðið mynstur
- safnar stöfum saman í lógíska röð
	- stafaraðirnar kallast les (lexeme)
	- borið kennsl á þau með mynstursgreiningu
- Úthlutar kóðum fyrir sérhvert les
	- kóðarnir kallaðir tókar (tokens)
	- flokkun á lesum
	- oft táknaðir með integer gildum
- Finnur les í inntakinu og skilar samsvarandi tóka til þess sem kallar (þáttarans)
	- sleppir comments og white space
- Endanleg stöðuvél (finite-state automaton)
	- ber kennsl á flokk mála sem kallast regluleg mál
	- hægt að tákna með stöðuriti (state diagram)

Þáttun (syntax analysis) parsing
- tvö ólík markmið í þáttun
	- athuga hvort forrit er setningafræðilega rétt
		- ef villa finnst þá eru villuskilaboð búin til og þáttun heldur áfram
	- Búa til þáttunartré
		- Stundum aðeins óbeint
- Tegundir
	- ofansækinn top-down
		- Safn endurkvæminna undirforrita
		- byggir þáttunartré á ofansækinn máta
		- sér undirforrit er skrifað fyrir sérhverja máleiningu í mállýsingunni
			- byggir þann hluta þáttunart´resins sem byrjar á viðeigandi máleiningu
			- undirforritið er þáttari fyrir mál (mengi af strengjum) sem hægt er að leiða út frá viðkomandi máleiningu
		- Tré byggt á þann hátt að byrjarð er í rótinni og haldið áfram niður að laufunum (tókunum)
		- Þáttunartréð byggt í preorder
			- jafngildir vinstri afleiðslu
		- Vinstri setningaform er á sniðinu xAa
			- x -> strengur af tókum (terminal symbols)
			- A -> máleining (non-terminal)
			- a -> blandaður strengur
			- Stækka þarf A næst til að búa til næsta setningaform í vinstri afleiðslu
			- velja þarf réttu málregluna sem hefur A sem vinstri hlið.
	- neðansækinn bottom-up
		- þáttunartréð er byggt á þann hátt að byrjað er í laufunum (tókunum) og haldið áfram upp að rótinni

Parsing decision problem
- þáttari þarf að velja reglu til að beita
- Algengast að nota fyrstu tókana í inntakinu sem hægt er að leiða út úr máleiningunni sem á að stæka

LL málfræðiflokkurinn (grammar class
- left to right scan & leftmost derivation
- Ekki hægt að skrifa LL þáttara fyrir allar mállýsingar
- A -> A + B
	- óendanleg endurkvæmni
	- líka A-> BaA og B->Ab saman

Vinstri þáttun (left factoring) -> er thing

Forritunarmál
- gervimál notuð til að tjá reiknirit.


Leiðir til að lýsa máli
- málfræði
- merking
- Málnotkunarfræði


Málfræði
- hvaða orð/setningar/frasar eru réttir (í málinu)?
	- Lesgreining ber kennsl á röð stafa sem mynda orð eða tóka
	- Málskipan lýsir því hvaða röð af tókum mynda löglegar setningar / frasa

Merking
- hvaða merking liggur í löglegri setningu?
	- Merking forrita er auðveldari en náttúrulegra mála

Málnotkunarfræði (pragmatics)
- Hvernið notum við merkingarbærar setningar?
	- Setningar með sömu merkingu geta verið notaðar á mismunandi hátt af mismunandi notendum
	- Mismunandi málfræðilegt samhengi getur kallað fram notkun á mismunandi setningum

Útfærsla
- Aðeins í forritunarmálum
- HVernig keyrum við löglega setningu á þann máta að tekið sé tillit til merkingar hennar


Málskipan
- Erfitt að lýsa með náttúrulegu tungumáli -> margræðni
- Context-free grammar CFG (Samhengisfrjáls mállýsing)
	- Aðferð til að lýsa setningafræðilegum fyrirbærum á formlegan hátt (Noam Chomsky)
- hugtök
	- ef Mengið A er stafróf þá er A\* mengi allra endanlegra strengja yfir A (kleene's star)
	- Runa af lengdinni 0 er einnig hluti f A\* -> táknaður með €
	- Formlegt mál yfir stafrófið A er í raun ekkert annað en hlutmengi í A\*
- stöff
	- vinstri afleiðsla -> byrja vinstra megin
	- hægri afleiðsla   -> byrja hægra megin


Samhengisfrjáls Mállýsing
- fernd (NT, T, R S) (G = (NT, T, R, S))
	- NT 
		- endanlegt mengi af táknum (non-terminals, setningaflokkar)
	- T 
		- endanlegt mengi af táknum (terminals, tókum)
	- R
		- endanlegt mengi af reglum (productions) þar sem hver þeirra er á forminu V -> w
	- S
		- stak í NT (start symbol)
- Strengir myndaðir með afleiðslu (derivation)
- v => w
- w er leiddur af v og skrifum v =\*> w ef til er endanleg (mögulega tóm) runa af tafarlausum afleiðslum

Myndað mál (generated language)
- Málið sem mállýsingin G myndar er megnið L(G) = { w € T\* | S =\*> w}

Þáttunartré
- Fyrir mállýsingu G = (NT, T, R, S) er þáttunartré raðað þar sem
	- Sérhver hnútur er merktur með tákni úr NT U T U {€}
	- Rótin er merkt með S
	- Sérhver millihnútur er merktur með tákni úr NT
	- afleiðsla gerð með reglum frá foreldri í barn P => C
	- Ef hnútur hefur merkinguna € þá er sá hnútur "einbirni". Ef A er foreldri þess hnútar þá er A -> €
- Lægra í trénu = meiri forgangur

| ![Screenshot 2024-04-24 at 10.58.16.png](../images/Screenshot%202024-04-24%20at%2010.58.16.png) | ![Screenshot 2024-04-24 at 10.56.55.png](../images/Screenshot%202024-04-24%20at%2010.56.55.png) |
| ------------------------------------------ | ------------------------------------------ |
|                                            |                                            |

Margræðni
- Mállýsing er margræð ef til er a.m.k. einn strengur L(G) sem hægt er að mynda með fleiri en einu þáttunartré
	- Þar af leiðandi ónothæf sem lýsing á forritunarmáli L því hana er ekki hægt að nota til að þýða forrit í L á einkvæman hátt

![Screenshot 2024-04-24 at 11.03.41.png](../images/Screenshot%202024-04-24%20at%2011.03.41.png)
![Screenshot 2024-04-24 at 11.03.54.png](../images/Screenshot%202024-04-24%20at%2011.03.54.png)

Setningafræðileg skylirði háð samhengi
- Strengir sem eru löglegir m.t.t. mállýsingar eru aðeins löglegir í tilteknu samhengi
	- td. Int = Real + 3 -> tag segðar á hægri hlið er ekki það sama og tag breytu á vinstri hlið.
- dæmi
	- tag breytur þarf að vera skilgreint fyrir notkun hennar
	- fjöldi raunstika í fallakalli þarf að stemma við fjölda leppa
	- í tilviki gildisveitingar þarf tag segðar að passa við tag breytunnar á vinstri hlið
	- að gefa stýribreytu for lykkju nýtt gildi er ekki leyfilegt
	- áður en breyta er notuð þarf að vera búið að gefa henni upphafsgildi


Samhengisháð mállýsing (context-sensitive grammer)
- Skilyrði háð samhengi má ekki lýsa með context-free grammar
- Samhengisháð mállýsing er til (erfitt að skrifa og engar aðferðir til að mynda þýðanda á skilvirkan hátt út frá þessum mállýsingum)

Raunstikar - actual parameters
leppar -> formal parameters


Þýðandi
- hvernig er hægt að nota mállýsingu til að þýða forrit
- Nota þýðanda sem er útfærður m.t.t. mállýsingar. Þýðandi samanstendur af runu af forritseiningum.
- Þýðandinn tekur inn 
	- streng
	- texta frumforritsins (source language) 
	- myndar ýmsar milliniðurstöður eða milliþulu
	- þangað til strengur í markmálinu hefur verið myndaður
		- markmál getur verið high-level eða low-level![Screenshot 2024-04-24 at 11.10.53.png](../images/Screenshot%202024-04-24%20at%2011.10.53.png)


Lesgreining (lexical analysis (scanning))
- les einstaka stafi sem mynda forritstextann og tekur þá saman í merkingarbærar einingar sem kallast tókar (tokens)
- Frátekin orð í málinu, virkjar, svigar eru dæmi um tóka
- Inniheldur ekki tékk hvort röð tóka myndi löglegar setningar


Þáttun (syntactic analysis (parsins))
- Athugar hvort runa tóka myndi löglega setningu
- Reynir að mynda (stundum óbeint) þáttunartré þar sem lauf trésins samsvara tókunum frá lesgreininum.
- Syntax error ef ekki er hægt að mynda þáttunartré

Lesgreining og þáttun eru samofing
- lesgreinirinn er í raun fall sem þáttarinn notar til að sækja næsta tóka.

Merkingargreining (semantic analysis)
- Þáttunartréð, sem stendur fyrir löglegt inntak, er notað til að tékka ýmis samhengisháð skilyrði í málinu.
	- Skilgreiningar, tög, fjölda viðfanga í fallakalli, o.s.frv.
- Þáttunartréð er skreytt með merkingafræðilegum upplýsingum
- Sérhver tóki sem stendur fyrir breytu er skreyttur með tagi
- Upplýsingar um breytur eru geymdar í sérstakri gagnaskipan sem kallast nafnatafla (symbol table)


Myndun milliþulu (intermediate code)
- fyrsti fasi þulusmíðinnar (code generation)
- Á þessu stigi er þula í markmálinu ekki búin til því það er hægt að framvkæma ýmis konar bestun (optimization) ssem er óháð viðkomandi markmáli
- Milliþulan er hönnuð til að vera óháð bæði frummálinu og markmálinu
	- Þýðandi er oft útfærður til að geta myndað kóða fyrir margar tegundir markmála.

Þulubestu (code optimization)
- Hægt að framkvæma bestun áður en endanleg smíði þulu í markmálinu á sér stað
	- fjarlægja ónotaðan kóða
	- in-line expansion af function calls
	- bestun á lykkjum

Þulusmíði
- þula í markmálinu er mynduð út frá milliþulu sem hefur verið bestuð
- síðasti fasi bestunar er háður sérstökum eiginleikum markmálsins / vélbúnaðarins
- í þýðanda, sem myndar vélarmálskóða, er mikilvægt lokaskref: register assignment

Sýndarvél
- Tölva sem keyrir reiknirit sem sett eru fram á formlegan hátt
- Sýndarvél eða hugræn vél er útdráttur af hugtakinu tölva
	- Sýndarvél keyrir forrit skref fyrir skref
- sýndarvél er hugræn (abstract) vegna þess að hún sleppir mörgum smáatriðum sem eru til staðar í tölvum.
- Reiknirit sem við viljum keyra eru sett fram með því að nota skipanir í tilteknu forritunarmáli L
- Málskipan (syntax) L gerir okkur kleift að nota tiltekið mengi af skipunum til að skrifa forrit

Sýndarvél
- Látum L vera forritunarmál
- Sýndarvél fyrir L táknuð með ML samanstendur af mengi af gagnaskipan og reikniritum sem geta séð um minnisúthlutun og keyrslu forrits sem skrifað er í L
- Þegar forritunarmálið L er ekki tekið fram, þá tölum við einfaldlega um sýndarvél M og sleppum lágvísunum




Túlkur
- 
	- 

Execution cycle of a generic interpreter



Vélarmál (machine language)
- Fyrir gefna sýndarvél ML þá er málið L sem túlkurinn fyrir ML skilur kallað vélarmál ML

Vélbúnaður (hardware machine)
- útfærður með rökrásum og rafeindahlutum
- Köllum þess konar vél MHlh þar sem lh er vélarmál hennar
- hlutir
	- minni
		- gögn samsett af grunttögum
		- öll gögn sett fram sem runur af bitum
	- vélarmál
		- Einfaldar skipanir
		- Skipanir og gögn geymd á tilteknu sniði
		- mengi mögulegra skipana er háð undirliggjandi vél
	- túlkur
		- Aðgerðir : reikni- og rökaðgerðir
		- Stýring á röð aðgerða (sequence control)
			- program counter geymir vistfangið á næstu skipun sem á að keyra
		- Gagnaflutningur
			- ákveðin gisti notuð til að vinna með aðalminni
		- Minnismeðhöndlun
			- háð undirliggjandi vél
				- Einfaldasta tilvik: forriti er hlaðið upp í minni, það byrjar strax keyrslu og er í minni þangað til það hættir keyrslu
				- einhvers konar samhliða vinnsla er yfirleitt alltaf til staðar keyrslu forrits getur verið frestað til að gefa öðru forriti aðgang að örgjörvanum
		- Útfærður sem mengi af vélbúnaðareiningum sem mynda örgjörvann
		- styður við keyrsluna á fetch-decode-execute cycle

Fetch-decode-execute cycle
- fetch
	- næsta skipun sem á að keyra er sótt úr minni
	- virki og þolendur er geymd í instruction gistinu
- Decode
	- Skipunin í instruction gistinum er afkóðuð með sérstökum rökrásum. Þolendurnir eru sóttir með gagnaflutningsaðgerðum með því að nota vistfangshaminn sem kemur fram í skipuninni
- Execute
	- grunnaðgerð (primitive hardware operation) er framkvæmd. Gagnaflutningsaðgerðir sjá um að koma gögnum til og frá minni.

Útfærsla á forritunarmáli
- ML er skv. skilgreiningu vél sem gerir kleift að keyra forrit sem skrifað er í L
- Sýndarvél samsvarar því tilteknu máli þ.e. vélarmáli hennar
- á hinn bóginn, fyrir gefið forritunarmál L geta margar sýndarvélar haft L sem sitt vélarmál
	- Sýndarvélarnar geta verið ólíkar á þann hátt hvernig túlkurinn er útfærður og hvaða gagnaskipan þær nota.
	- Þær eiga hins vegar allar það sameiginlegt að þær túlka sama málið L
	- Fer eftir útfærslu
- AÐ útfæra forritunarmál L þýðir að útfæra sýndarvél sem hefur L sem sitt vélarmál


Útfærsla á sýndarvél
- útfærsla í vélbúnaði
	- Vélbúnaður útfærir þá gagnaskipan og þau reiknirit sem ML þarfnast
	- Eingöngu low-level forritunarmál notuð vegna þess að skipanir / sentningar þeirra eiga sér beint samræmi í aðgerðum í vélbúnaði.
	- kostir
		- keyrsla forrits í L er hröð
	- Ókostir
		- setningar / segðir high-level forritunarmáls L eru tiltölulega flóknar og langt frá þeirri grundvallarvirkni sem á sér stað í vélbúnaði
		- Að breyta þess konar vél (sem þegar hefur verið útfærð) yrði nánast ómögulegt. a.m.k. kostnaðarsamar
- Hermun með hugbúnaði
	- Nota forrit skrifað í öðru máli L' til að útfæra þá gagnaskipan og þau reiknirit sem ML þarfnast
	- með því að nota M'L' vélina fyrir L' er hægt að útfæra vélina ML með viðeigandi forritum skrifuðum í L'
		- þessi forrit túlka setningar í L með því að herma eftir virkninni í ML
	- Kostir
		- sveigjanleiki
			- Forritum sem útfæra virkni í ML er auðveldlega hægt að breyta
	- ókostir
		- skilvirkni
			- overhead (fjöldi aðgerða fyrir eina skipun (hugsanlega))
			- Hægari en vélbúnaðarútfærsla vegna þess að útfærslan á ML notar aðara Sýndarvél M'L' sem þarf að vera útfærð
- Hermun með fastbúnaði (firmware)
	- Hermun á gagnaskipna og reikniritum í ML í microcode
	- svipað og hermun með hugbúnaði - hermt er eftir ML með því að nota forrit. í þessu tilviki með því að nota fastbúnað, forrit sem eru microforrit en ekki forrit skrifuð í high-level máli
	- Microforrit
		- skrifuð í sérstökum low-level málum og eru geymd í sérstöku read-only minni
			- mjög hraðvirk m.v. hugbúnaðarútfærslu
			- Flókið að breyta í microcode og þarfnast sérstaks vélbúnaarð til að endurskrifa í read-only minni

tegundir útfærslu
- Fyrir útfærsluna á ML höfum við aðgang að MoLo (host machine) útfærslan á L með MoLo á sér stað með því að þýða L yfir í LO
- hrein túlkuð útfærsla
	- Forrit er útfært í Lo sem túlkar allar skipanir í L. Þetta forrit er túlkur ILo|L
- hrein þýdd útfærsla
- eitthvað þar á milli
![Screenshot 2024-04-24 at 11.58.16.png](../images/Screenshot%202024-04-24%20at%2011.58.16.png)


Hreint túlkuð útfærsla
- Þetta er ekki raunveruleg þýðing því kóði sem samsvarar skipun í L er keyrður beint af túlkinum en ekki skrifaður út
- Túlkur fyrir mál L, skrifaður í máli LO er forrit sem útfærir hlutskilgreint fall (partial function)
	- ILo|L : (ProgL X D) -> D such that ILo|L (PL, Input) = PL(input)ILo|L mengi af skipunum í LO sem samsvara skipunum í málinu L
- Kostir
	- Sveigjanleiki: Auðvelt að þróa aflúsara (debugger)
	- auðveldara að útfæra túlk heldur en þýðanda
- ókostur
	- óskilvirkni
		- Túlkurinn ILO|L þarf að framkvæma afkóðun á setningum / segðum í L á meðan á keyrslu stendur
		- Hluti af tímanum sem það tekur að keyra P^L, inniheldur tímann sem fer í að framkvæma afkóðun

![Screenshot 2024-04-24 at 12.08.41.png](../images/Screenshot%202024-04-24%20at%2012.08.41.png)


Hrein þýdd útfærsla
- Þýðandi sem þýðir L yfir í Lo er forrit sem útfærir fall
	- CL,LO : Prog^L -> Prog^LO
- Þ.a. fyrir gefið forrit P^L ef CL,Lo(P^L) = Pc^Lo þá gildir fyrir sérhvert input € D
	- P^L(input) = Pc^Lo(input)
- Eiginleikar
	- L er kallað frummál (source language) og LO kallað markmál (object language)
	- Til að keyra forrit P^L skrifað í L á inntakið D, þá er CL,LO fyrst keyrt með P^L sem inntak
	- Þýðingarferlið er sem sagt sérstakt ferli, óháð keyrsluferlinu.
- Kostur
	- skilvirkni
		- þarf ekki að eyða tíma í afkóðun í keyrslu
		- þýðing á skipun í forriti P^L á sér stað einu sinni óháð því hversu oft forritið er keyrt
- ókostir
	- Þýðingaferlið týnir upplýsingum um uppbyggingu frumforritsins
		- þegar keyrsluvilla (runtime error) á sér stað getur verið erfitt að ákvarða hvaða setning / lína í frumforritinu veldur 
	- erfiðara að útfæra aflúsara

Túlkun
- Túlkur vinnur oft með innri framsetningu forrits sem er frábrugðin þeirri ytri
- Vörpunin úr ytri framsetningu á forriti í L yfir á innri framsetningu er gerð með því að þýða L yfir á millimál (intermediate language)
- millimálið er það sem er túlkað


Þýðing
- Sumar skipanir fyrir inntak/úttak eru oft þýddar yfir í stýriskerfisköll sem þá herma eftir high-level skipunum á keyrslutíma.


Raunveruleikinn
- ![Screenshot 2024-04-24 at 12.22.08.png](../images/Screenshot%202024-04-24%20at%2012.22.08.png)
- Túlka þau atriði sem eru lengst frá máli host machine en þýða restina
- þýðing er mikilvæg þegar keyrsluhraði skiptir miklu máli
- túlkun er æskileg þegar sveigjanleiki er í fyrirrúmi


Interpretive compilers
- þýða forrit yfir á millimál
- útfæra (túlka) millimálið á hinum mismunandi verkvöngum.

Flytjanleiki
- fyrst gert í Pascal, með því að nota P-code sem milimál
- notað í Java, -> java virtual machine og samsvarandi vélarmál er Java Byte Code


Bootstrapping
- Process
	- Devise minimal subset of a language
	- write a compiler for that minimal subset in the language of that minimal subset
	- hand translate this minimal subsett source code into assembly language and assemble it - this produces a working compiler for a subset of the target language
	- write a new compiler in the language of the working compiler to accept more source features that are missing from the language of the workign comeppiler
	- user the working compiler to compile this new compiler - this prduces a new working compiler which accepts a superset of the language under which it was compiled
	- repeat the last two steps until the working comipler realizes all features in the soruce language








Af hverju er rangt að segja að mál sé þýtt eða túlkað
- hægt er að útfæra sérhvert forritunarmál með þvi að nota annað hvort þýðanda eða túlk.
- það er útfærsluatriði
	- það er hægt að búa til python þýðanda
	- og það er hægt að útfæra C túlk



