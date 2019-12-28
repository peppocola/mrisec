1)Illustrare in maniera sintetica i problemi dei recommender systems di tipo content-based.

<br><br>
		**many of the same /overspecialization** := rischio di raccomandazioni ripetitive con scarsa novelty/serendipity per via della sovraspecializzazione del recommender
		<br>
		**new user** := non conosco i gusti del nuovo utente quindi non so cosa raccomandargli
		<br>
		**limited content analisys** := un item potrebbe essere descritto in generale senza fare menzione delle feature più importanti, che potrebbe portare a raccomandare l'item quando non dovrebbe o proprio a non essere mai raccomandato
<br><br><br>
2)Illustrare in maniera sintetica i problemi dei recommender systems di tipo collaborativo.

<br><br>
		**matrice sparsa per i rating** := difficile trovare dei vicini
		se un utente non esprime preferenze non può avere raccomandazioni
		<br>
		**cold-start** := senza community non c'è modo di raccomandare (ma si possono usare altri approcci)
		<br>
		**new-user** := non può avere raccomandazioni
		<br>
		**new-item** := un nuovo item non ha preferenze di alcun utente e dunque non può essere raccomandato
		<br>
		**grey-sheep** := difficile trovare utenti simili significativi se un utente valuta in modo "intermedio" ogni item, non si sbilancia nel valutare.
		<br>
		**"canto delle sirene"(SEMERARO TRADEMARK)** := valutazioni false o organizzate alterano lo stato del sistema e influenzano le raccomandazioni
<br><br><br>
3)Descrivere le metriche di errore (MAE ed RMSE) utilizzate per la valutazione dell’accuratezza dei recommender systems.

<br><br>
	**MAE** := Mean Absolute Error, calcola la deviazione tra i rating predetti e i rating reali
<br>
	**RMSE** := Root Mean Square Error, come MAE ma penalizza deviazioni più grandi utilizzando il quadrato della differenza tra rating predetto e rating attuale

![](./img/mae_rmse.PNG)
<br><br><br>
4)Descrivere, commentando opportunamente, la funzione per il calcolo delle predizioni dei rating in un algoritmo di filtraggio collaborativo di tipo user-to-user.

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
5)Illustrare in maniera sintetica il problema della overspecialization (sovraspecializzazione) dei content-based recommender systems

6)Illustrare in maniera sintetica il problema del Cold-start nei recommender systems di tipo collaborativo

<br><br><br>
7)Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione ricorsiva basata sul “flow” model.

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
8)Descrivere in maniera sintetica i concetti fondamentali alla base del modello dei dati RDF, in particolare i concetti di risorsa, proprietà e statement.

<br><br>
	il modello dei dati RDF è basato su tre concetti:
	<br>
	 – **Risorse**: tutto ciò che viene descritto, ogni risorsa è identificata da un URI
	<br>
	 – **Proprietà**: una coppia attributo-valore che si vuole associare ad una risorsa, l'attributo è anch'esso identificato da un URI e il valore può essere un'altra risorsa o un tipo di dato primitivo (stringa, intero...)
	<br>
	 – **Asserzioni o statement**: l’associazione di una proprietà ad una risorsa, ci dice che “una risorsa (soggetto) ha un certo valore (oggetto) per una certa proprietà (predicato)”

<br><br><br>
9)Descrivere il problema dello spider trap nell’algoritmo PageRank e illustrare una possibile soluzione.

<br><br>
	**spider trap**: se nel grafo ci sono dei cicli i nodi coinvolti nel ciclo assorbono l'importanza e non è garantita la convergenza dell' algoritmo<br>
	una possibile soluzione è data dal random teleport<br>
	**random teleport**: ad ogni istante si segue un link con probabilita b e si salta ad una pagina casuale con probabilita 1-b.<br>
	(b in range(0.8, 0.9))<br>

10)Descrivere i principali problemi dell’algoritmo PageRank e illustrare una possibile soluzione.

<br><br>
	**spider trap**: se nel grafo ci sono dei cicli, i nodi coinvolti nel ciclo assorbono l'importanza e non è garantita la convergenza dell'algoritmo<br>
	**dead end**: se c'e un nodo senza archi uscenti l'algoritmo converge ma tutte le pagine avranno importanza 0.<br>
	entrambi i problemi si risolvono con il **random teleport**: ad ogni istante si segue un link con probabilita b e si salta ad una pagina casuale con probabilita 1-b (b in range[0.8, 0.9])

<br><br><br>
11)Descrivere in maniera sintetica il concetto di reificazione degli statement RDF.

<br><br>
	**reificazione** significa riduzione ad oggetto dell'asserzione. Si utilizza la reificazione per esprimere meta-informazioni su una meta-informazione. Quindi l'oggetto della tripla Soggetto-Proprietà-Oggetto diventa uno statement, quindi una tripla Soggetto-Proprietà-Oggetto.
	Dopo avere reificato l’asserzione si potranno esprimere ulteriori proprietà su di essa.

<br><br><br>
12)Descrivere in maniera sintetica i principi alla base del PageRank, focalizzando l’attenzione sulla formulazione basata su matrici di adiacenza stocastiche

<br><br>
	**INTRO**
	Il web viene visto come un grafo orientato dove i nodi rappresentano le pagine web e gli archi rappresentano i link tra le pagine.
	Per il rank delle pagine si sfrutta la struttura del grafo (link entranti e uscenti da ogni nodo)
	<br><br>
	**MATRIX FORMULATION**:<br>
	In questa formulazione si costruisce a partire dal grafo una matrice di adiacenza stocastica
	dove se la pagina I ha Di link uscenti allora
	se i->j allora Mji=1/Di altrimenti Mji=0.<br>
	Dato r un vettore con un valore per ogni pagina:
	ri è l' importanza della pagina i.<br>
	La somma dei valori di r=1<br>
	![](./img/rank_sum.PNG)<br>
	quindi data M:matrice di adiacenza e r:vettore dei rank le "equazioni di flusso"
	possono essere scritte come ***r=M*r***.<br>
	Cosi facendo abbiamo trasformato il problema del ranking nel problema di ricerca di un autovettore per la matrice M.<br>
	L'autovettore che cerchiamo è quello associato all'autovalore 1 (il fatto che la matrice M sia stocastica ci assicura l'esistenza di tale autovettore).<br>
	Inoltre possiamo risolvere questo problema in modo efficiente con il metodo delle power iteration:<br>
	![](./img/rank_power.PNG)
