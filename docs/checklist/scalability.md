---
title: "Elenco di controllo per la scalabilità"
description: "Indicazioni sull'elenco di controllo per la scalabilità per le problematiche di progettazione relative alla scalabilità automatica di Azure."
author: dragon119
ms.date: 03/24/2017
ms.custom: checklist
ms.openlocfilehash: 250fa2d56720c476bb604c5dba684e938088b6a0
ms.sourcegitcommit: b0482d49aab0526be386837702e7724c61232c60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2017
---
# <a name="scalability-checklist"></a>Elenco di controllo per la scalabilità
[!INCLUDE [header](../_includes/header.md)]

## <a name="service-design"></a>Progettazione dei servizi
* **Partizionare il carico di lavoro**. Progettare le diverse parti del processo in modo che siano discrete e scomponibili. Ridurre il più possibile le dimensioni di ogni parte, attenendosi comunque alle solite regole di separazione dei compiti e al principio di responsabilità singola. Questo consente di distribuire le parti in modo da ottimizzare l'uso di ogni unità di calcolo, ad esempio server di database o ruoli. Facilita anche la scalabilità dell'applicazione con l'aggiunta di altre istanze di risorse specifiche. Per altre informazioni, vedere le [indicazioni sul partizionamento delle risorse di calcolo](https://msdn.microsoft.com/library/dn589773.aspx).
* **Progettare per la scalabilità**. La scalabilità consente alle applicazioni di reagire a un carico variabile aumentando o diminuendo il numero di istanze dei ruoli, delle code e di altri servizi usati. L'applicazione deve tuttavia essere progettata tenendo presente tale necessità. Ad esempio, l'applicazione e i servizi che usa devono essere senza stato per consentire il routing delle richieste a qualsiasi istanza. Ciò evita anche che l'aggiunta o la rimozione di istanze specifiche si ripercuota negativamente sugli utenti correnti. È anche consigliabile implementare la configurazione o il rilevamento automatico delle istanze man mano che vengono aggiunte o rimosse, in modo che il codice nell'applicazione possa eseguire il routing necessario. Ad esempio, un'applicazione Web potrebbe usare un set di code secondo un approccio round robin per instradare le richieste ai servizi in background in esecuzione in ruoli di lavoro. L'applicazione Web deve riuscire a rilevare le modifiche nel numero di code per instradare correttamente le richieste e bilanciare il carico dell'applicazione.
* **Scalare come unità**. Pianificare altre risorse per far fronte alla crescita. Per ogni risorsa verificare i limiti massimi di scalabilità e usare il partizionamento orizzontale o la scomposizione per superare tali limiti. Determinare le unità di scala per il sistema in termini di set di risorse ben definiti. In questo modo, l'uso di operazioni per l'aumento delle istanze risulterà più semplice e avrà meno probabilità di incidere negativamente sull'applicazione a seguito delle limitazioni derivanti dalla mancanza di risorse in una parte del sistema generale. Ad esempio, se si aggiunge un numero x di ruoli Web e di lavoro, potrebbero essere necessari y code aggiuntive e z account di archiviazione per gestire il carico di lavoro aggiuntivo generato dai ruoli. Un'unità di scala può quindi essere costituita da x ruoli Web e di lavoro, *y* code e *z* account di archiviazione. Progettare l'applicazione in modo che possa essere ridimensionata facilmente aggiungendo una o più unità di scala.
* **Evitare l'affinità client**. Se possibile, assicurarsi che l'applicazione non richieda l'affinità. In tal modo, le richieste possono essere indirizzate a qualsiasi istanza e il numero di istanze è irrilevante. Questo inoltre evita il sovraccarico dovuto all'archiviazione, al recupero e alla gestione delle informazioni sullo stato per ogni utente.
* **Sfruttare le funzionalità di scalabilità automatica della piattaforma**. Se la piattaforma di hosting supporta una funzionalità di scalabilità automatica, ad esempio la scalabilità automatica di Azure, preferirla a meccanismi personalizzati o di terze parti, a meno che il meccanismo incorporato non possa soddisfare i requisiti. Ove possibile, usare regole di scalabilità pianificata per garantire la disponibilità delle risorse senza ritardi di avvio, ma aggiungere alle regole una scalabilità automatica reattiva (quando opportuno) per gestire variazioni impreviste della domanda. È possibile usare le operazioni di scalabilità automatica nell'API Gestione dei servizi per adeguare la scalabilità automatica e aggiungere contatori personalizzati alle regole. Per altre informazioni, vedere [Indicazioni sulla scalabilità automatica](../best-practices/auto-scaling.md).
* **Eseguire l'offload delle attività a elevato utilizzo di CPU/IO come attività in background**. Se si prevede che una richiesta a un servizio comporti una lunga esecuzione o assorba una quantità considerevole di risorse, eseguire l'offload dell'elaborazione relativa alla richiesta a un'attività separata. Usare ruoli di lavoro o processi in background (a seconda della piattaforma di hosting) per eseguire queste attività. Tale strategia consente al servizio di continuare a ricevere altre richieste restando reattivo.  Per altre informazioni, vedere le [indicazioni sui processi in background](../best-practices/background-jobs.md).
* **Distribuire il carico di lavoro per le attività in background**. Se sono presenti numerose attività in background o se le attività richiedono una notevole quantità di tempo o risorse, suddividere il lavoro tra più unità di calcolo, ad esempio ruoli di lavoro o processi in background. Per una possibile soluzione, vedere l'articolo relativo al [modello di consumer concorrenti](https://msdn.microsoft.com/library/dn568101.aspx).
* **Considerare la possibilità di passare a un'architettura *senza condivisione*.** Un'architettura "shared-nothing" usa nodi indipendenti e autosufficienti privi di punti di contesa, ad esempio risorse di archiviazione o servizi condivisi. In teoria un sistema di questo tipo può essere scalato quasi all'infinito. Anche se un approccio totalmente di tipo "shared-nothing" non è in genere pratico per la maggior parte delle applicazioni, può offrire opportunità per progettare una migliore scalabilità. Ad esempio, evitare l'uso dello stato della sessione sul lato server, l'affinità client e il partizionamento dei dati rappresentano buoni esempi di transizione verso un'architettura "shared-nothing".

## <a name="data-management"></a>Gestione dei dati
* **Usare il partizionamento dei dati**. Suddividere i dati tra più database e server di database oppure progettare l'applicazione per l'uso di servizi di archiviazione dati che forniscano tale partizionamento in modo trasparente, ad esempio un database elastico per il database SQL di Azure e l'archivio tabelle di Azure. Questo approccio può contribuire a ottimizzare le prestazioni e consente di implementare più facilmente la scalabilità. Sono disponibili diverse tecniche di partizionamento, ad esempio orizzontale, verticale e funzionale. È possibile usare una combinazione di esse per ottenere i massimi vantaggi dal miglioramento delle prestazioni delle query, una scalabilità semplificata, una gestione più flessibile e una maggiore disponibilità e per adattare il tipo di archivio ai dati che dovrà contenere. Considerare inoltre l'eventualità di usare tipi diversi di archivio dati per tipi diversi di dati, effettuando la scelta in base al modo in cui sono ottimizzati per il tipo di dati specifico. Questo può includere l'uso dell'archivio tabelle, di un database di documenti o di un archivio dati di tipo famiglia di colonne al posto o insieme a un database relazionale. Per altre informazioni, vedere le [indicazioni sul partizionamento dei dati](../best-practices/data-partitioning.md).
* **Progettare ai fini della coerenza finale**. La coerenza finale migliora la scalabilità riducendo o eliminando il tempo necessario per sincronizzare i dati correlati partizionati in più archivi. Lo svantaggio è rappresentato dal fatto che i dati non sono sempre coerenti al momento della lettura e che alcune operazioni di scrittura possono causare conflitti. La coerenza finale è ideale per le situazioni in cui gli stessi dati vengono letti frequentemente, ma scritti raramente. Per altre informazioni, vedere l'articolo di [introduzione alla coerenza dei dati](https://msdn.microsoft.com/library/dn589800.aspx).
* **Ridurre le interazioni "frammentate" tra componenti e servizi**. Evitare di progettare interazioni in cui un'applicazione deve effettuare più chiamate a un servizio, ognuna delle quali restituisce una piccola quantità di dati, invece di una singola chiamata che può restituire tutti i dati. Quando possibile, combinare diverse operazioni correlate in un'unica richiesta se la chiamata è relativa a un servizio o componente che presenta una latenza notevole. Questo rende più semplice il monitoraggio delle prestazioni e l'ottimizzazione delle operazioni complesse. Ad esempio, usare stored procedure nei database per incapsulare la logica complessa e ridurre il numero di round trip e il blocco delle risorse.
* **Usare le code per livellare il carico per le operazioni di scrittura dati ad alta velocità**. I picchi nella domanda di un servizio possono sovraccaricare tale servizio e causare una propagazione dei problemi. Per evitare tali situazioni, considerare la possibilità di implementare il [modello di livellamento del carico basato sulle code](https://msdn.microsoft.com/library/dn589783.aspx). Usare una coda che funge da buffer tra un'attività e un servizio richiamato. Questo può alleggerire i sovraccarichi a intermittenza che diversamente potrebbero causare un errore del servizio o il timeout dell'attività.
* **Ridurre al minimo il carico dell'archivio dati**. L'archivio dati in genere costituisce un collo di bottiglia per l'elaborazione, è una risorsa costosa e la scalabilità orizzontale può risultare difficoltosa. Dove possibile, rimuovere la logica, ad esempio l'elaborazione di documenti XML oppure oggetti JSON, dall'archivio dati ed eseguire l'elaborazione all'interno dell'applicazione. Ad esempio, anziché passare l'XML al database, in un formato diverso da una stringa opaca per l'archiviazione, è possibile serializzare o deserializzare l'XML all'interno del livello dell'applicazione e passarlo in un formato nativo all'archivio dati. In genere è molto più semplice aumentare le istanze dell'applicazione invece dell'archivio dati, quindi è consigliabile provare a eseguire la maggior parte possibile dell'elaborazione a elevato utilizzo di risorse di calcolo all'interno dell'applicazione.
* **Ridurre al minimo il volume dei dati recuperati**. Recuperare solo i dati necessari specificando le colonne e usando criteri per selezionare le righe. Usare i parametri con valori di tabella e il livello di isolamento appropriato. Usare meccanismi come i tag di entità per evitare di recuperare dati inutilmente.
* **Usare la memorizzazione nella cache in modo aggressivo**. Usare la memorizzazione nella cache laddove possibile per ridurre il carico delle risorse e dei servizi che generano o forniscono dati. La memorizzazione nella cache in genere è adatta per i dati relativamente statici o da ottenere con una notevole elaborazione. La memorizzazione nella cache deve avvenire a tutti i livelli appropriati in ogni livello dell'applicazione, tra cui l'accesso ai dati e la generazione dell'interfaccia utente. Per altre informazioni, vedere le [indicazioni sulla memorizzazione nella cache](../best-practices/caching.md).
* **Gestire l'aumento e la conservazione dei dati**. La quantità di dati archiviati da un'applicazione aumenta nel tempo. Questa crescita genera un aumento dei costi di archiviazione e della latenza durante l'accesso ai dati, influendo negativamente sulle prestazioni e sulla velocità effettiva dell'applicazione. È possibile archiviare periodicamente alcuni dati precedenti a cui non si accede più o spostare i dati a cui si accede raramente in un archivio a lungo termine più conveniente anche se la latenza di accesso è superiore.
* **Ottimizzare gli oggetti di trasferimento dati usando un formato binario efficiente**. Gli oggetti di trasferimento dati vengono passati più volte tra i livelli di un'applicazione. La riduzione delle dimensioni riduce il carico sulle risorse e sulla rete. Tuttavia, occorre bilanciare il risparmio con il sovraccarico che deriva dalla conversione dei dati nel formato richiesto in ogni posizione in cui viene usata. Adottare un formato che garantisca la massima interoperabilità per consentire di riutilizzare facilmente un componente.
* **Impostare il controllo cache**. Progettare e configurare l'applicazione per l'uso della memorizzazione nella cache dell'output o di frammenti, ove possibile, per ridurre al minimo il carico di elaborazione.
* **Abilitare la memorizzazione nella cache sul lato client**. Le applicazioni Web devono abilitare le impostazioni della cache per il contenuto che può essere memorizzato nella cache. La memorizzazione nella cache è disabilitata per impostazione predefinita. Configurare il server in modo che fornisca le intestazioni di controllo cache appropriate per consentire la memorizzazione del contenuto nella cache nei server proxy e nei client.
* **Usare l'archivio BLOB di Azure e la rete per la distribuzione di contenuti per ridurre il carico dell'applicazione**. Considerare la possibilità di archiviare il contenuto pubblico statico o relativamente statico, come immagini, risorse, script e fogli di stile, in un archivio BLOB. Questo approccio risparmia all'applicazione il carico causato dalla generazione dinamica di tale contenuto per ogni richiesta. Considerare inoltre l'eventualità di usare la rete per la distribuzione di contenuti per memorizzare nella cache questo contenuto e fornirlo ai client. L'uso della rete per la distribuzione di contenuti può migliorare le prestazioni a livello del client, perché il contenuto viene distribuito dal data center geograficamente più vicino che contiene una cache della rete per la distribuzione di contenuti. Per altre informazioni, vedere [Indicazioni sulla rete per la distribuzione di contenuti (CDN)](../best-practices/cdn.md).
* **Ottimizzare gli indici e le query SQL**. Alcuni costrutti o istruzioni T-SQL possono influire negativamente sulle prestazioni e tale impatto può essere ridotto ottimizzando il codice in una stored procedure. Ad esempio, evitare di convertire tipi **datetime** in **varchar** prima del confronto con un valore letterale **datetime**. Usare invece funzioni di confronto data/ora. L'assenza di indici appropriati può anche rallentare l'esecuzione delle query. Se si usa un framework ORM (Object/Relational Mapping), comprendere come funziona e come può incidere sulle prestazioni del livello di accesso ai dati. Per altre informazioni, vedere [Ottimizzazione delle query](https://technet.microsoft.com/library/ms176005.aspx).
* **Considerare la possibilità di denormalizzare i dati**. La normalizzazione dei dati consente di evitare la duplicazione e l'incoerenza. La gestione di più indici, la verifica dell'integrità referenziale, l'esecuzione di più accessi a piccoli blocchi di dati e l'unione di tabelle tramite join per riassemblare i dati sono tutte operazioni che generano un sovraccarico che può influire negativamente sulle prestazioni. Valutare se una certa duplicazione e un volume di archiviazione aggiuntivo sono accettabili per ridurre il carico dell'archivio dati. Allo stesso scopo, determinare anche se l'applicazione stessa, che in genere è più facile da ridimensionare, può essere considerata affidabile per l'esecuzione di attività come la gestione dell'integrità referenziale. Per altre informazioni, vedere le [indicazioni sul partizionamento dei dati](../best-practices/data-partitioning.md).

## <a name="service-implementation"></a>Implementazione dei servizi
* **Usare chiamate asincrone**. Quando possibile, usare codice asincrono per accedere a risorse o servizi che possono essere limitati da larghezza di banda di rete o I/O oppure che hanno una latenza considerevole per evitare di bloccare il thread chiamante. Per implementare le operazioni asincrone, usare il [Modello asincrono basato su attività (TAP)](https://msdn.microsoft.com/library/hh873175.aspx).
* **Evitare di bloccare le risorse e usare invece un approccio ottimistico**. Non bloccare mai l'accesso alle risorse, ad esempio di archiviazione o altri servizi che presentino una latenza notevole, perché è una delle cause principali della riduzione delle prestazioni. Usare sempre approcci ottimistici per la gestione delle operazioni simultanee, ad esempio la scrittura in un archivio. Usare le funzionalità del livello di archiviazione per gestire i conflitti. Nelle applicazioni distribuite i dati possono essere coerenti solo alla fine.
* **Comprimere i dati altamente comprimibili su reti a bassa larghezza di banda e latenza elevata**. Nella maggior parte dei casi, in un'applicazione Web il volume di dati più significativo generato dall'applicazione e passato attraverso la rete è costituito dalle risposte HTTP alle richieste client. La compressione HTTP può ridurre considerevolmente tale volume, soprattutto per il contenuto statico. Questa soluzione può ridurre i costi, nonché diminuire il carico sulla rete, anche se la compressione del contenuto dinamico applica un carico leggermente più elevato sul server. In altri ambienti più generalizzati la compressione dei dati può ridurre il volume dei dati trasmessi e ridurre al minimo i tempi e costi di trasferimento, ma comporta un sovraccarico per i processi di compressione e decompressione. Deve pertanto essere usata solo quando si ottiene un miglioramento dimostrabile delle prestazioni. Altri metodi di serializzazione, come la codifica binaria o JSON, possono ridurre le dimensioni del payload e allo stesso tempo generare un impatto più limitato sulle prestazioni, mentre è probabile che l'XML ne causi l'aumento.
* **Ridurre al minimo il tempo di utilizzo delle connessioni e delle risorse**. Mantenere le connessioni e le risorse soltanto per il tempo necessario a usarle. Ad esempio, aprire le connessioni solo all'ultimo momento e restituirle al pool di connessioni appena possibile. Acquisire le risorse il più tardi possibile ed eliminarle il prima possibile.
* **Ridurre al minimo il numero di connessioni necessarie**. Le connessioni ai servizi assorbono risorse. Limitare il numero di connessioni necessarie e assicurarsi che le connessioni esistenti vengano riutilizzate quando possibile. Ad esempio, dopo l'autenticazione, usare la rappresentazione se appropriato per eseguire codice come un'identità specifica. Questo consente un uso ottimale del pool di connessioni mediante il riutilizzo delle stesse.
  
  > [!NOTE]
  > Le API per alcuni servizi riutilizzano automaticamente le connessioni fornite e condizione che siano seguite le linee guida specifiche del servizio. È importante comprendere le condizioni che consentono di riutilizzare la connessione per ogni servizio usato dall'applicazione.
  > 
  > 
* **Inviare le richieste in batch per ottimizzare l'uso della rete**. Ad esempio, inviare e leggere i messaggi in batch quando si accede a una coda ed eseguire più operazioni di lettura o scrittura come batch durante l'accesso all'archiviazione o a una cache. Questo consente di massimizzare l'efficienza dei servizi e degli archivi dati riducendo il numero di chiamate sulla rete.
* **Evitare l'archiviazione dello stato della sessione sul lato server come requisito** laddove possibile. La gestione dello stato della sessione sul lato server richiede in genere l'affinità client, ovvero il routing di ogni richiesta alla stessa istanza del server, il che incide sulla possibilità di ridimensionare il sistema. Idealmente è consigliabile progettare i client in modo che siano senza stato rispetto ai server che usano. Se però l'applicazione deve mantenere lo stato della sessione, archiviare i dati riservati o i grandi volumi di dati per client in una cache del lato server distribuita a cui possano accedere tutte le istanze dell'applicazione.
* **Ottimizzare gli schemi di archiviazione tabelle**. Quando si usano archivi tabelle che richiedono il passaggio e l'elaborazione dei nomi di tabelle e colonne con ogni query, ad esempio l'archivio tabelle di Azure, considerare la possibilità di usare nomi più brevi per ridurre tale sovraccarico. Non sacrificare tuttavia la leggibilità o la gestibilità usando nomi eccessivamente compatti.
* **Usare Task Parallel Library (TPL) per eseguire operazioni asincrone**. La libreria TPL semplifica la scrittura di codice asincrono che esegue operazioni associate all'I/O. Usare *ConfigureAwait(false)* ove possibile per eliminare la dipendenza di una continuazione in un contesto di sincronizzazione specifico. In questo modo si riduce la possibilità che si verifichino deadlock del thread.
* **Creare dipendenze delle risorse durante la distribuzione o all'avvio dell'applicazione**. Evitare chiamate ripetute ai metodi che verificano l'esistenza di una risorsa e quindi creano la risorsa se non esiste. I metodi come *CloudTable.CreateIfNotExists* e *CloudQueue.CreateIfNotExists* nella libreria client di Archiviazione di Azure seguono questo modello. Tali metodi possono generare un notevole sovraccarico se vengono richiamati prima di ogni accesso a una tabella o coda di archiviazione. In alternativa:
  * Creare le risorse necessarie quando l'applicazione viene distribuita o viene avviata per la prima volta. È accettabile avere una singola chiamata a *CreateIfNotExists* per ogni risorsa nel codice di avvio per un ruolo Web o di lavoro. Assicurarsi tuttavia di gestire le eccezioni che possono venire generate se il codice prova ad accedere a una risorsa inesistente. In queste situazioni è consigliabile registrare l'eccezione e avvisare l'operatore della mancanza di una risorsa.
  * In alcune circostanze, può essere opportuno creare la risorsa mancante come parte del codice di gestione delle eccezioni. Tuttavia, è consigliabile adottare questo approccio con cautela, perché l'assenza della risorsa potrebbe essere indicativa di un errore di programmazione, ad esempio, un nome di risorsa con errori di ortografia, o di un altro problema a livello di infrastruttura.
* **Usare framework semplificati**. Scegliere con attenzione le API e i framework da usare per ridurre al minimo l'utilizzo delle risorse, il tempo di esecuzione e il carico complessivo dell'applicazione. Ad esempio, l'uso dell'API Web per gestire le richieste di servizio consente di ridurre il footprint dell'applicazione e aumentare la velocità di esecuzione, ma potrebbe non essere adatta per scenari avanzati in cui sono necessarie le funzionalità aggiuntive di Windows Communication Foundation.
* **Considerare la possibilità di ridurre al minimo il numero degli account del servizio**. Ad esempio, usare un account specifico per accedere alle risorse o ai servizi che impongono un limite per le connessioni o che vengono eseguiti in modo più efficiente dove vengono mantenute meno connessioni. Questo approccio è comune per i servizi, come ad esempio i database, ma può compromettere la possibilità di controllare accuratamente le operazioni a causa della rappresentazione dell'utente originale.
* **Effettuare la profilatura delle prestazioni e il testing del carico** durante lo sviluppo come parte delle routine di test e prima del rilascio della versione finale per assicurarsi che l'applicazione venga eseguita e scalata come richiesto. Questo testing deve essere eseguito sullo stesso tipo di hardware disponibile nella piattaforma di produzione e con gli stessi tipi e quantità di dati e carico utente che si riscontreranno in produzione. Per altre informazioni, vedere [Test delle prestazioni di un servizio cloud](/azure/vs-azure-tools-performance-profiling-cloud-services/).
