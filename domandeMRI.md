***Se trovi qualche errore o puoi suggerire qualche miglioria, fallo inviando una pull-request oppure segnalamelo in qualche modo, grazie***

Lista Domande:<br>
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
[12](#12))Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione basata su matrici di adiacenza stocastiche


# 1
Illustrare in maniera sintetica i problemi dei recommender systems di tipo content-based.

<br><br>
		**Many of the same/Overspecialization** := I recommender system di tipo content-based non hanno un metodo per trovare qualcosa di nuovo. Il sistema suggerisce gli item che, quando confrontati con il profilo dell'utente, hanno un punteggio alto. Quindi all'utente saranno raccomandati gli item simili a quelli gia votati. Questo inconveniente è chiamato serendipity problem che evidenzia la tendenza dei sistemi basati sui contenuti a produrre raccomandazioni con un limitato grado di novita. Per dare un esempio, quando un utente ha valutato solo i film di Harry Potter, ricevera raccomandazioni solo per quel tipo di film. Una tecnica content-based perfetta raramente proporra qualcosa di nuovo, limitando cosi le applicazioni per le quali potrebbe essere utile.
		<br>
		**New user** := Prima che un recommender system di tipo content-based possa realmente capire le preferenze di un utente e fornire delle raccomandazioni accurate, deve collezionare un numero sufficiente di ratings. Quando sono disponibili pochi ratings il sistema non sarà in grado di fornire raccomandazioni affidabili.
		<br>
		**Limited Content Analisys** := un item potrebbe essere descritto in generale senza fare menzione delle feature più importanti, che potrebbe portare a il sistema a raccomandare l'item quando non dovrebbe o proprio a non essere mai raccomandato.
		<br>
		Nessun content-based recommender system può fornire delle raccomandazioni affidabili se il contenuto analizzato non ha abbastanza informazioni per distinguere gli item che piacciono all'utente rispetto a quelli che non gradisce. Alcune rappresentazioni hanno solamente alcuni aspetti e ne tralasciano altri che potrebbero influenzare l'esperienza dell'utente
		<br>
		In conclusione, assegnare manualmente o automaticamente le features all'item potrebbe non essere sufficiente per distuinguere gli aspetti dell'item che sono necessari per l'elicitazione degli interessi dell'utente

<br><br><br>
# 2
Illustrare in maniera sintetica i problemi dei recommender systems di tipo collaborativo.

<br><br>
		**Matrice sparsa per i rating** := difficile trovare dei vicini
		se un utente non esprime preferenze non può avere raccomandazioni
		<br>
		**Cold-start** := In un recommender system di tipo collaborativo, è essenziale avere una community che valuta gli item per poter effettuare delle raccomandazioni. senza community non c'è modo di raccomandare item e si devono utilizzare approcci differenti (es: content-based o raccomandare oggetti popolari).
		<br>
		**New-user** := Un nuovo utente non può avere alcuna raccomandazione con questo approccio fino a quando non esprime almeno una preferenza. Tuttavia le raccomandazioni saranno poco accurate fino a quando l'utente non fornirà un buon numero di preferenze.
		<br>
		**New-item** := Un nuovo item non ha alcuna preferenza espressa da alcun utente e non verrà raccomandato fino a quando non ci sarà qualche utente che lo valuterà.
		<br>
		**Gray-sheep** :=	difficile trovare utenti simili significativi se un utente valuta con rating neutrali ogni item, non si sbilancia nel valutare. ***&ast;***
		<br>
		**"Canto delle sirene"(SEMERARO TRADEMARK)** := valutazioni false o organizzate alterano lo stato del sistema e influenzano le raccomandazioni ***&ast;***
		<br><br>
		***&ast;= la risposta è approssimativa e stiamo cercando delle risposte migliori***
<br><br><br>
# 3
Descrivere le metriche di errore (MAE ed RMSE) utilizzate per la valutazione dell’accuratezza dei recommender systems.

<br><br>
	**MAE** := Mean Absolute Error, calcola la deviazione tra i rating predetti e i rating reali
<br>
	**RMSE** := Root Mean Square Error, come MAE ma penalizza deviazioni più grandi utilizzando il quadrato della differenza tra rating predetto e rating attuale

![](./img/mae_rmse.PNG)
<br><br><br>
# 4
Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo user-to-user.

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
	Un approccio puo essere quello di usare la inverse user frequency
	<br>
	![](./img/u2u_inverseUser.PNG)
	<br>
	![](./img/u2u_FWPC.PNG)
	<br>

<br><br><br>
# 5
Illustrare in maniera sintetica il problema della overspecialization (sovraspecializzazione) dei content-based recommender systems

<br><br>
	I recommender system di tipo content-based non hanno un metodo per trovare qualcosa di nuovo. Il sistema suggerisce gli item che, quando confrontati con il profilo dell'utente, hanno un punteggio alto. Quindi all'utente saranno raccomandati gli item simili a quelli gia votati. Questo inconveniente è chiamato serendipity problem che evidenzia la tendenza dei sistemi basati sui contenuti a produrre raccomandazioni con un limitato grado di novita. Per dare un esempio, quando un utente ha valutato solo i film di Harry Potter, ricevera raccomandazioni solo per quel tipo di film. Una tecnica content-based perfetta raramente proporra qualcosa di nuovo, limitando cosi le applicazioni per le quali potrebbe essere utile.
	<br>

<br><br><br>
# 6
Illustrare in maniera sintetica il problema del Cold-start nei recommender systems di tipo collaborativo

<br><br>
	Prima che un recommender system di tipo content-based possa realmente capire le preferenze di un utente e fornire delle raccomandazioni accurate, deve collezionare un numero sufficiente di ratings. Quando sono disponibili pochi ratings il sistema non sarà in grado di fornire raccomandazioni affidabili.

<br><br><br>
# 7
Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione ricorsiva basata sul “flow” model.

<br><br>
	**INTRO**
	Il web viene visto come un grafo orientato dove i nodi rappresentano le pagine web e gli archi rappresentano i link tra le pagine.
	Per il rank delle pagine si sfrutta la struttura del grafo (link entranti e uscenti da ogni nodo)
	<br>
	**FLOW MODEL**
	I link vengono visti come voti, l'importanza di un link è proporzionale all' importanza della pagina da cui proviene. In particolare il peso di un link è dato dall' importanza della pagina diviso l'out degree della pagina.
	L'importanza di una pagina è data dalla somma dei voti su i suoi link entranti.
	<br>
	![](./img/rank_flow.PNG)
	<br>
	se costruiamo le "equazioni di flusso" per un grafo otteniamo n equazioni in n incognite
	e questo non permette di avere una soluzione unica, per risolvere questo problema
	si aggiunge un ulteriore vincolo che permette l'unicità (r1+r2+...+rn=1)
	Questa formulazione funziona bene con piccoli grafi ma non è scalabile.<br>
	quini abbiamo bisogno di una nuova formulazione ovvero la **MATRIX FORMULATION**

<br><br><br>
# 8
Descrivere in maniera sintetica i concetti fondamentali alla base del modello dei dati RDF, in particolare i concetti di risorsa, proprietà e statement.

<br><br>
	il modello dei dati RDF è basato su tre concetti:
	<br>
	 – **Risorse**: tutto ciò che viene descritto, ogni risorsa è identificata da un URI
	<br>
	 – **Proprietà**: una coppia attributo-valore che si vuole associare ad una risorsa, l'attributo è anch'esso identificato da un URI e il valore può essere un'altra risorsa o un tipo di dato primitivo (stringa, intero...)
	<br>
	 – **Asserzioni o statement**: l’associazione di una proprietà ad una risorsa, ci dice che “una risorsa (soggetto) ha un certo valore (oggetto) per una certa proprietà (predicato)”

<br><br><br>
# 9
Descrivere il problema dello spider trap nell’algoritmo PageRank e illustrare una possibile soluzione.

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

<br><br><br>
# 10
Descrivere i principali problemi dell’algoritmo PageRank e illustrare una possibile soluzione.

<br><br>
	**(1) (Stanford University)**<br>
	<br>
	**Spider Trap**: un gruppo di una o più pagine che non hanno alcun link che porta a nodi che non appartengono al gruppo. in questo caso i nodi appartenenti al gruppo accumuleranno tutta l'importanza del Web. 	
	<br>
	**Dead End**: : una pagina che non ha successori (link uscenti) non può inviare la sua importanza a nessun nodo. In questo caso tutta l'importanza fuoriuscirà dal web(tutti i nodi avranno importanza 0).
	<br><br>
	Una soluzione ad entrambi i problemi è quella di "tassare" ogni pagina di una frazione della sua importanza(solitamente 0.2) e distribuire l'importanza tassata in modo uguale verso tutte le pagine (**Random Teleport**)
	<br><br>
	**(2) (Grisulli)**<br>
	<br>
	**Spider Trap**: se nel grafo c'è un gruppo di nodi che sono collegati solo tra loro, senza alcun modo di raggiungere nodi al di fuori del gruppo, questi nodi assorbono l'importanza e non è garantita la convergenza dell' algoritmo.
	<br><br>
	**Dead End**: se c'e un nodo senza archi uscenti l'algoritmo converge ma tutte le pagine avranno importanza 0.<br><br>
	entrambi i problemi si risolvono con il **Random Teleport**: ad ogni istante si segue un link con probabilita b e si salta ad una pagina casuale con probabilita 1-b (b in range[0.8, 0.9])

<br><br><br>
# 11
Descrivere in maniera sintetica il concetto di reificazione degli statement RDF.

<br><br>
	**Reificazione** significa riduzione ad oggetto dell'asserzione. Si utilizza la reificazione per esprimere meta-informazioni su una meta-informazione. Quindi l'oggetto della tripla Soggetto-Proprietà-Oggetto diventa uno statement, quindi una tripla Soggetto-Proprietà-Oggetto.
	Dopo avere reificato l’asserzione si potranno esprimere ulteriori proprietà su di essa.

<br><br><br>
# 12
Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione basata su matrici di adiacenza stocastiche

<br><br>
	**INTRO**
	Il web viene visto come un grafo orientato dove i nodi rappresentano le pagine web e gli archi rappresentano i link tra le pagine.
	Per il rank delle pagine si sfrutta la struttura del grafo (link entranti e uscenti da ogni nodo)
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
