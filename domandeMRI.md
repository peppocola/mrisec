***Se trovi qualche errore o puoi suggerire qualche miglioria, fallo inviando una pull-request oppure segnalamelo in qualche modo, grazie***

# Contributors
- [GreenSully](https://github.com/GreenSully)
- [NaimarDL](https://github.com/NaimarDL)
- [Ocen5](https://github.com/Ocen5)
- [paologas91](https://github.com/paologas91)
- [pasqualedem](https://github.com/pasqualedem)
- [peppocola](https://github.com/peppocola)


# Lista Domande

[1](#1))Illustrare in maniera sintetica i problemi dei recommender systems di tipo content-based.
<br><br>
[2](#2))Illustrare in maniera sintetica i problemi dei recommender systems di tipo collaborativo.
<br><br>
[3](#3))Descrivere le metriche di errore (MAE ed RMSE) utilizzate per la valutazione dell’accuratezza dei recommender systems.
<br><br>
[4](#4))Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo user-to-user.
<br><br>
[5](#5))Illustrare in maniera sintetica il problema della overspecialization (sovraspecializzazione) dei content-based recommender systems
<br><br>
[6](#6))Illustrare in maniera sintetica il problema del Cold-start nei recommender systems di tipo collaborativo
<br><br>
[7](#7))Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione ricorsiva basata sul “flow” model.
<br><br>
[8](#8))Descrivere in maniera sintetica i concetti fondamentali alla base del modello dei dati RDF, in particolare i concetti di risorsa, proprietà e statement.
<br><br>
[9](#9))Descrivere il problema dello spider trap nell’algoritmo PageRank e illustrare una possibile soluzione.
<br><br>
[10](#10))Descrivere i principali problemi dell’algoritmo PageRank e illustrare una possibile soluzione.
<br><br>
[11](#11))Descrivere in maniera sintetica il concetto di reificazione degli statement RDF.
<br><br>
[12](#12))Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione basata su matrici di adiacenza stocastiche.
<br><br>
[13](#13))Elencare similiarità e differenze tra sistemi di Information Filtering e Information Retrieval ***NEW***
<br><br>
[14](#14))Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo item-to-item. ***NEW***
<br><br>


# 1
**Illustrare in maniera sintetica i problemi dei recommender systems di tipo content-based.**

<br><br>
		**More of the same/Overspecialization** := I recommender system di tipo content-based non hanno un metodo per trovare qualcosa di nuovo. Il sistema suggerisce gli item che, quando confrontati con il profilo dell'utente, hanno un punteggio alto. Quindi all'utente saranno raccomandati gli item simili a quelli gia votati. Questo inconveniente è chiamato serendipity problem che evidenzia la tendenza dei sistemi basati sui contenuti a produrre raccomandazioni con un limitato grado di novita. Per dare un esempio, quando un utente ha valutato solo i film di Harry Potter, ricevera raccomandazioni solo per quel tipo di film. Una tecnica content-based perfetta raramente proporra qualcosa di nuovo, limitando cosi le applicazioni per le quali potrebbe essere utile.
		<br>
		**New user** := Prima che un recommender system di tipo content-based possa realmente capire le preferenze di un utente e fornire delle raccomandazioni accurate, deve collezionare un numero sufficiente di ratings. Quando sono disponibili pochi ratings il sistema non sarà in grado di fornire raccomandazioni affidabili.
		<br>
		**Limited Content Analisys** := (un item potrebbe essere descritto in generale senza fare menzione delle feature più importanti. Ciò potrebbe portare il sistema a raccomandare l'item quando non dovrebbe essere raccomandato o a non essere mai raccomandato.) (?)
		<br>
		Nessun content-based recommender system può fornire delle raccomandazioni affidabili se il contenuto analizzato non ha abbastanza informazioni per distinguere gli item che piacciono all'utente rispetto a quelli che non gradisce. Alcune rappresentazioni hanno solamente alcuni aspetti e ne tralasciano altri che potrebbero influenzare l'esperienza dell'utente
		<br>
		In conclusione, assegnare manualmente o automaticamente le features all'item potrebbe non essere sufficiente per distuinguere gli aspetti dell'item che sono necessari per l'elicitazione degli interessi dell'utente.


[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 2
**Illustrare in maniera sintetica i problemi dei recommender systems di tipo collaborativo.**

<br><br>
		**Matrice sparsa per i rating** :=  il problema della sparsità è comune alla maggior parte dei recommender system perchè solitamente gli utenti valutano solo una piccola parte degli item disponibili. Ciò è aggravato dal fatto che gli utenti e gli item appena aggiunti al sistema non avranno alcuna valutazione (cold-start). Quando la matrice è sparsa, due utenti o item raramente hanno valutazioni in comune e gli approcci neighborhood-based prediranno le valutazioni usando dei set di vicini molto piccoli. Questo porterà a delle raccomandazioni non affidabili.
		<br>
		**Cold-start** := In un recommender system di tipo collaborativo, è essenziale avere una community che valuta gli item per poter effettuare delle raccomandazioni. Senza community non c'è modo di raccomandare item e si devono utilizzare approcci differenti (es: content-based o raccomandare oggetti popolari, forzare utenti a valutare item, default voting).
		<br>
		**New-user** := Un nuovo utente non può avere alcuna raccomandazione con questo approccio fino a quando non esprime almeno una preferenza. Se non esprime delle preferenze, non può essere "vicino" di alcun altro utente. Tuttavia le raccomandazioni saranno poco accurate fino a quando l'utente non fornirà un buon numero di preferenze.
		<br>
		**New-item** := Un nuovo item non ha alcuna preferenza espressa da alcun utente. Quindi non risulterà neighbor di nessun altro oggetto nel caso item-to-item. Anche nel caso user-to-user sarà impossibile effettuare predizioni per alcun utente su quell'item perchè nessun'altro utente risulterà neighbor dell'utente su cui vogliamo calcolare la predizione.  Un new-item non verrà raccomandato fino a quando non ci sarà qualche utente che lo valuterà.
		<br>
		**Gray-sheep** := un utente le cui opionioni non concordano o discordano con alcun gruppo di persone. Ciò rende impossibile trovare un set significativo di neighbors e quindi di effettuare raccomandazioni specifiche. un utente "gray sheep" non si sbilancia nel valutare e valuta in modo neutrale la maggior parte o la totalità degli item.
		<br>
		**"Canto delle sirene"(SEMERARO TRADEMARK)** := valutazioni false o organizzate alterano lo stato del sistema e influenzano le raccomandazioni. Si possono creare profili fake o arruolare utenti per cercare di aumentare la valutazione complessiva di uno o più prodotti e diminuire quella dei competitors.
		<br>Lo scopo di questo attacco è manipolare "l'opinione" della comunità attaccata, promuovendo o contrastando la diffusione di un prodotto. E' possibile contrastare questi attacchi tramite l'analisi dei comportamenti degli utenti: nel caso di fake si avranno evidenti variazioni dalla media delle valutazioni degli items, oltre che una percentuale di ratings dell'80% circa (molto maggiore  rispetto ad utenti normali). Altre contromisure economiche sono l'uso di captcha o altri metodi di inserimento manuale, che però non funzionano in caso di arruolamento di utenti dietro compenso.
		<br><br>

[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 3
**Descrivere le metriche di errore (MAE ed RMSE) utilizzate per la valutazione dell’accuratezza dei recommender systems.**

<br><br>
	**MAE** := Mean Absolute Error, calcola la deviazione tra i rating predetti e i rating reali
<br>
	**RMSE** := Root Mean Square Error, come MAE ma penalizza deviazioni più grandi utilizzando il quadrato della differenza tra rating predetto e rating attuale

![](./img/mae_rmse.PNG)

[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 4
**Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo user-to-user.**

<br><br>
	Per predire i rating in un recommender system collaborativo di tipo user-to-user, dato un utente attivo(Alice) e un item(I) non ancora visto da Alice, si trova l'insieme degli utenti a cui sono piaciuti gli stessi item piaciuti ad Alice nel passato e che hanno valutato l'item I(neighbors).<br>
	Si puo utilizzare la media dei rating dei neighbors per predire il rating che Alice dara all'item I. L'idea è che se gli utenti hanno avuto gusti simili nel passato, avranno gusti simili nel futuro.
	<br>
	Si puo migliorare la predizione pesando i rating degli utenti con la loro similarita con Alice anziche utilizzare la semplice media. Si puo utilizzare una qualsiasi metrica di similarita ma le piu usate sono la similarita del coseno e il coeficiente di correlazione di Pearson.
	<br>
	![](./img/u2u_pearson.PNG)
	<br>Una formula comunemente usata per calcolare le predizioni è la seguente
	<br>
	![](./img/u2u_prediction.PNG)
	<br>
	che tiene conto dello stile di valutazione degli utenti piuttosto che il valore numerico del rating.
	<br>Si puo migliorare la predizione pesando maggiormente gli utenti che hanno piu item in comune
	<br>
	![](./img/u2u_co-rated.PNG)
	<br>penalizzando quelli che hanno un numero di item in comune minore di una certa soglia.
	<br>
	Inoltre si pesa maggiormente il rating su un item controverso piuttosto che uno su un item con scarsa varianza sui rating. (utilizzare la varianza)
	<br>
	Un approccio puo essere quello di usare la inverse user frequency.
	<br>
	![](./img/u2u_inverseUser.PNG)
	<br>
	![](./img/u2u_FWPC.PNG)
	<br>
	Per la selezione dei neighbors utilizzare un numero fissato di vicini o una soglia di similiarità.


[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 5
**Illustrare in maniera sintetica il problema della overspecialization (sovraspecializzazione) dei content-based recommender systems**

<br><br>
	I recommender system di tipo content-based non hanno un metodo per trovare qualcosa di nuovo. Il sistema suggerisce gli item che, quando confrontati con il profilo dell'utente, hanno un punteggio alto. Quindi all'utente saranno raccomandati gli item simili a quelli gia votati. Questo inconveniente è chiamato serendipity problem che evidenzia la tendenza dei sistemi basati sui contenuti a produrre raccomandazioni con un limitato grado di novita. Per dare un esempio, quando un utente ha valutato solo i film di Harry Potter, ricevera raccomandazioni solo per quel tipo di film. Una tecnica content-based perfetta raramente proporra qualcosa di nuovo, limitando cosi le applicazioni per le quali potrebbe essere utile.
	<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 6
**Illustrare in maniera sintetica il problema del Cold-start nei recommender systems di tipo collaborativo**

<br><br>
	Prima che un recommender system di tipo collaborativo possa realmente capire le preferenze di un utente e fornire delle raccomandazioni accurate, deve collezionare un numero sufficiente di ratings. Quando sono disponibili pochi ratings il sistema non sarà in grado di fornire raccomandazioni affidabili.
	In un recommender system di tipo collaborativo, è essenziale avere una community che valuta gli item per poter effettuare delle raccomandazioni. Senza community non c'è modo di raccomandare item e si devono utilizzare approcci differenti (es: content-based o raccomandare oggetti popolari, forzare utenti a valutare item, default voting).
	<br>
	**New-user** := Un nuovo utente non può avere alcuna raccomandazione con questo approccio fino a quando non esprime almeno una preferenza. Se non esprime delle preferenze, non può essere "vicino" di alcun altro utente. Tuttavia le raccomandazioni saranno poco accurate fino a quando l'utente non fornirà un buon numero di preferenze.
	<br>
	**New-item** := Un nuovo item non ha alcuna preferenza espressa da alcun utente. Quindi non risulterà neighbor di nessun altro oggetto nel caso item-to-item. Anche nel caso user-to-user sarà impossibile effettuare predizioni per alcun utente su quell'item perchè nessun'altro utente risulterà neighbor dell'utente su cui vogliamo calcolare la predizione.  Un new-item non verrà raccomandato fino a quando non ci sarà qualche utente che lo valuterà.
	<br>
	<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 7
**Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione ricorsiva basata sul “flow” model.**

<br><br>
	**INTRO**<br>
	Il web viene visto come un grafo orientato dove i nodi rappresentano le pagine web e gli archi rappresentano i link tra le pagine. Non si tiene conto del contenuto delle pagine.<br>
	Per il rank delle pagine si sfrutta la struttura del grafo (link entranti e uscenti da ogni nodo).
	<br><br>
	**FLOW MODEL**<br>
	L'importanza della pagina è data dalla topologia del grafo:
	<br>- Una pagina è importante se puntata da tante pagine (link entranti) o da pagine con molta importanza.
	<br>- Una pagina trasferisce importanza attraverso i link uscenti e lo fa in maniera proporzionale al numero di link uscenti che possiede.                           
	<br>
	I link vengono visti come voti, l'importanza di un link è proporzionale all' importanza della pagina da cui proviene. In particolare il peso di un link è dato dall' importanza della pagina diviso l'out degree della pagina.
	L'importanza di una pagina è data dalla somma dei voti/pesi su i suoi link entranti.
	<br>
	![](./img/rank_flow.PNG)
	<br>
	Se costruiamo le "equazioni di flusso" per un grafo otteniamo n equazioni in n incognite. Questo non permette di avere una soluzione unica. Per risolvere questo problema si aggiunge un ulteriore vincolo che permette l'unicità ***(r1+r2+...+rn=1)***.
	In questo modo si può risolvere il sistema di equazioni con l'Eliminazione di Gauss che funziona bene con piccoli grafi ma non è scalabile.<br>
	Quindi abbiamo bisogno di una nuova formulazione ovvero la **MATRIX FORMULATION**
	<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 8
**Descrivere in maniera sintetica i concetti fondamentali alla base del modello dei dati RDF, in particolare i concetti di risorsa, proprietà e statement.**

<br><br>
	il modello dei dati RDF è basato su tre concetti:
	<br>
	 – **Risorse**: tutto ciò che viene descritto, ogni risorsa è identificata da un URI
	<br>
	 – **Proprietà**: una coppia attributo-valore che si vuole associare ad una risorsa, l'attributo è anch'esso identificato da un URI e il valore può essere un'altra risorsa o un tipo di dato primitivo (stringa, intero...)
	<br>
	 – **Asserzioni o statement**: l’associazione di una proprietà ad una risorsa, ci dice che “una risorsa (soggetto) ha un certo valore (oggetto) per una certa proprietà (predicato)”
	 <br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 9
**Descrivere il problema dello spider trap nell’algoritmo PageRank e illustrare una possibile soluzione.**

<br><br>
	**(1) (Stanford University)**<br>
	<br>
	**Spider Trap**: un gruppo di una o più pagine che non hanno alcun link che porta a nodi che non appartengono al gruppo. in questo caso i nodi appartenenti al gruppo accumuleranno tutta l'importanza del Web. 	
	<br>
	Una soluzione è quella di "tassare" ogni pagina di una frazione della sua importanza(solitamente 0.2) e distribuire l'importanza tassata in modo uguale verso tutte le pagine (**Random Teleport**)
	<br><br>
	**(2) (Grisulli)**<br>
	<br>
	**Spider Trap**: se nel grafo c'è un gruppo di nodi che sono collegati solo tra loro, senza alcun modo di raggiungere nodi al di fuori del gruppo, questi nodi assorbono l'importanza e non è garantita la convergenza dell' algoritmo.<br>
	<br>
	Una soluzione può essere il
	**Random Teleport**: ad ogni istante si segue un link con probabilita b e si salta ad una pagina casuale con probabilita 1-b.<br>
	(b in range(0.8, 0.9))<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 10
**Descrivere i principali problemi dell’algoritmo PageRank e illustrare una possibile soluzione.**

<br><br>
	**(1) (Stanford University)**<br>
	<br>
	**Spider Trap**: un gruppo di una o più pagine che non hanno alcun link che porta a nodi che non appartengono al gruppo. in questo caso i nodi appartenenti al gruppo accumuleranno tutta l'importanza del Web. 	
	<br>
	**Dead End**: una pagina che non ha successori (link uscenti) non può inviare la sua importanza a nessun nodo. In questo caso tutta l'importanza fuoriuscirà dal web(tutti i nodi avranno importanza 0).
	<br><br>
	Una soluzione ad entrambi i problemi è quella di "tassare" ogni pagina di una frazione della sua importanza(solitamente 0.2) e distribuire l'importanza tassata in modo uguale verso tutte le pagine (**Random Teleport**)
	<br><br>
	**(2) (Grisulli)**<br>
	<br>
	**Spider Trap**: se nel grafo c'è un gruppo di nodi che sono collegati solo tra loro, senza alcun modo di raggiungere nodi al di fuori del gruppo, questi nodi assorbono l'importanza e non è garantita la convergenza dell' algoritmo.
	<br><br>
	**Dead End**: se c'e un nodo senza archi uscenti l'algoritmo converge ma tutte le pagine avranno importanza 0.<br><br>
	entrambi i problemi si risolvono con il **Random Teleport**: ad ogni istante si segue un link con probabilita b e si salta ad una pagina casuale con probabilita 1-b (b in range[0.8, 0.9])
	<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 11
**Descrivere in maniera sintetica il concetto di reificazione degli statement RDF.**

<br><br>
	**Reificazione** significa riduzione ad oggetto dell'asserzione. Si utilizza la reificazione per esprimere meta-informazioni su una meta-informazione. Quindi l'oggetto della tripla Soggetto-Proprietà-Oggetto diventa uno statement, quindi una tripla Soggetto-Proprietà-Oggetto.
	Dopo avere reificato l’asserzione si potranno esprimere ulteriori proprietà su di essa. <br>
	(Soggetto-Predicato-(Soggetto-Predicato-Oggetto))
	<br>
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 12
**Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione basata su matrici di adiacenza stocastiche**

<br><br>
	**INTRO**
	Il web viene visto come un grafo orientato dove i nodi rappresentano le pagine web e gli archi rappresentano i link tra le pagine. Non si tiene conto del contenuto delle pagine.
	Per il rank delle pagine si sfrutta la struttura del grafo (link entranti e uscenti da ogni nodo).
	<br><br>
	**MATRIX FORMULATION**:<br>
	In questa formulazione si costruisce a partire dal grafo una matrice di adiacenza stocastica sulle colonne. (la somma delle colonne è 1)<br>
 	Se la pagina I ha ***Di*** link uscenti allora:<br>
		Se i->j allora ***Mji=1/Di*** altrimenti ***Mji=0***.<br><br>
	Dato r un vettore con un valore per ogni pagina:
	***ri*** è l' importanza della pagina i.<br>
	La somma dei valori di r è 1<br>
	![](./img/rank_sum.PNG)<br><br>
	Siano:<br>
	***M***:matrice di adiacenza <br>
	***r***:vettore dei rank <br>
	Le "equazioni di flusso" possono essere scritte come ***r=M&ast;r***.<br>
	Cosi facendo abbiamo trasformato il problema del ranking nel problema di ricerca di un ***autovettore*** per la matrice M.<br>
	L'autovettore che cerchiamo è quello associato all'***autovalore 1*** (il fatto che la matrice M sia stocastica ci assicura l'esistenza di tale autovettore).<br>
	Inoltre possiamo risolvere questo problema in modo efficiente con il metodo delle power iteration:<br>
	![](./img/rank_power.PNG)
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 13
**Elencare similiarità e differenze tra sistemi di Information Filtering e Information Retrieval**

<br><br>

***SEZIONE IN LAVORAZIONE***
[Torna alla lista...](#Lista-Domande)
<br><br><br>
# 14
**Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo item-to-item.**

<br><br>

***SEZIONE IN LAVORAZIONE***
[Torna alla lista...](#Lista-Domande)
<br><br><br>
