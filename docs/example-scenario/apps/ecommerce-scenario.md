---
title: Front-end per e-commerce in Azure
description: Scenario comprovato di hosting di un sito di e-commerce in Azure
author: masonch
ms.date: 7/13/18
ms.openlocfilehash: 568821e97c6b90a36429dfa8ec0ef9ed38c7963c
ms.sourcegitcommit: 71cbef121c40ef36e2d6e3a088cb85c4260599b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2018
ms.locfileid: "39060972"
---
# <a name="e-commerce-front-end-on-azure"></a><span data-ttu-id="445ae-103">Front-end per e-commerce in Azure</span><span class="sxs-lookup"><span data-stu-id="445ae-103">E-Commerce front-end on Azure</span></span>

<span data-ttu-id="445ae-104">Questo scenario di esempio descrive l'implementazione di un front end di e-commerce usando gli strumenti della piattaforma distribuita come servizio (PaaS) di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-104">This example scenario walks you through an implementation of an e-commerce front end using Azure Platform-as-a-Service (PaaS) tools.</span></span> <span data-ttu-id="445ae-105">Molti siti di e-commerce sono soggetti a stagionalità e variabilità del traffico nel tempo.</span><span class="sxs-lookup"><span data-stu-id="445ae-105">Many e-commerce websites face seasonality and traffic variability over time.</span></span> <span data-ttu-id="445ae-106">Quando la richiesta di prodotti o servizi decolla, in modo prevedibile o imprevedibile, l'uso di strumenti PaaS consente di gestire più clienti e più transazioni automaticamente.</span><span class="sxs-lookup"><span data-stu-id="445ae-106">When demand for your products or services takes off, whether predictably or unpredictably, using PaaS tools will allow you to handle more customers and more transactions automatically.</span></span> <span data-ttu-id="445ae-107">Questo scenario sfrutta inoltre l'economia del cloud, pagando solo la capacità effettivamente usata.</span><span class="sxs-lookup"><span data-stu-id="445ae-107">Additionally, this scenario takes advantage of cloud economics by paying only for the capacity you use.</span></span>

<span data-ttu-id="445ae-108">Questo documento illustra i diversi componenti di Azure PaaS e le considerazioni relative alla distribuzione di un'applicazione di e-commerce di esempio, *Relecloud Concerts*, ovvero una piattaforma online per l'acquisto di biglietti per concerti.</span><span class="sxs-lookup"><span data-stu-id="445ae-108">This document will help you will learn about various Azure PaaS components and considerations used to bring together to deploy a sample e-commerce application, *Relecloud Concerts*, an online concert ticketing platform.</span></span>

## <a name="potential-use-cases"></a><span data-ttu-id="445ae-109">Potenziali casi d'uso</span><span class="sxs-lookup"><span data-stu-id="445ae-109">Potential use cases</span></span>

<span data-ttu-id="445ae-110">Prendere in considerazione questo scenario per i casi d'uso seguenti:</span><span class="sxs-lookup"><span data-stu-id="445ae-110">Consider this scenario for the following use cases:</span></span>

* <span data-ttu-id="445ae-111">Compilazione di un'applicazione che necessita di scalabilità elastica per gestire i picchi di utenti in momenti diversi.</span><span class="sxs-lookup"><span data-stu-id="445ae-111">Building an application that needs elastic scale to handle bursts of users at different times.</span></span>
* <span data-ttu-id="445ae-112">Compilazione di un'applicazione progettata per funzionare a disponibilità elevata in diverse aree di Azure in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="445ae-112">Building an application that is designed to operate at high availability in different Azure regions around the world.</span></span>

## <a name="architecture"></a><span data-ttu-id="445ae-113">Architettura</span><span class="sxs-lookup"><span data-stu-id="445ae-113">Architecture</span></span>

![Architettura dello scenario di esempio per un'applicazione di e-commerce][architecture-diagram]

<span data-ttu-id="445ae-115">Questo scenario descrive l'acquisto di biglietti da un sito di e-commerce. Il flusso di dati dello scenario è il seguente:</span><span class="sxs-lookup"><span data-stu-id="445ae-115">This scenario covers purchasing tickets from an e-commerce site, the data flows through the scenario as follows:</span></span>

1. <span data-ttu-id="445ae-116">Gestione traffico di Azure indirizza la richiesta di un utente al sito di e-commerce ospitato nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-116">Azure Traffic Manager routes a user's request to the e-commerce site hosted in Azure App Service.</span></span>
2. <span data-ttu-id="445ae-117">La rete CDN di Azure fornisce immagini e contenuti statici all'utente.</span><span class="sxs-lookup"><span data-stu-id="445ae-117">Azure CDN serves static images and content to the user.</span></span>
3. <span data-ttu-id="445ae-118">L'utente accede all'applicazione tramite un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="445ae-118">User signs in to the application through an Azure Active Directory B2C tenant.</span></span>
4. <span data-ttu-id="445ae-119">L'utente cerca i concerti usando la funzione Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-119">User searches for concerts using Azure Search.</span></span>
5. <span data-ttu-id="445ae-120">Il sito Web restituisce i dettagli dei concerti dal database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-120">Web site pulls concert details from Azure SQL Database.</span></span> 
6. <span data-ttu-id="445ae-121">Il sito Web fa riferimento alle immagini dei biglietti acquistati presenti in Archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="445ae-121">Web site refers to purchased ticket images in Blob Storage.</span></span>
7. <span data-ttu-id="445ae-122">I risultati delle query sul database vengono memorizzati nella Cache Redis di Azure per ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="445ae-122">Database query results are cached in Azure Redis Cache for better performance.</span></span>
8. <span data-ttu-id="445ae-123">L'utente invia ordini per biglietti e recensioni sul concerto che vengono inseriti nella coda.</span><span class="sxs-lookup"><span data-stu-id="445ae-123">User submits ticket orders and concert reviews which are placed in the queue.</span></span>
9. <span data-ttu-id="445ae-124">Funzioni di Azure elabora il pagamento dell'ordine e le recensioni sul concerto.</span><span class="sxs-lookup"><span data-stu-id="445ae-124">Azure Functions processes order payment and concert reviews.</span></span>
10. <span data-ttu-id="445ae-125">Servizi cognitivi fornisce un'analisi della recensione del concerto per determinare il sentimento (positivo o negativo).</span><span class="sxs-lookup"><span data-stu-id="445ae-125">Cognitive services provide an analysis of the concert review to determine the sentiment (positive or negative).</span></span>
11. <span data-ttu-id="445ae-126">Application Insights fornisce metriche delle prestazioni per il monitoraggio dell'integrità dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="445ae-126">Application Insights provides performance metrics for monitoring the health of the web application.</span></span>

### <a name="components"></a><span data-ttu-id="445ae-127">Componenti</span><span class="sxs-lookup"><span data-stu-id="445ae-127">Components</span></span>

* <span data-ttu-id="445ae-128">La [rete CDN di Azure][docs-cdn] fornisce contenuti statici memorizzati nella cache da posizioni vicine agli utenti per ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="445ae-128">[Azure CDN][docs-cdn] delivers static, cached content from locations close to users to reduce latency.</span></span>
* <span data-ttu-id="445ae-129">[Gestione traffico di Azure][docs-traffic-manager] consente di controllare la distribuzione del traffico degli utenti per gli endpoint del servizio in diverse aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-129">[Azure Traffic Manager][docs-traffic-manager] controls the distribution of user traffic for service endpoints in different Azure regions.</span></span>
* <span data-ttu-id="445ae-130">[Servizi app - App Web][docs-webapps] ospita applicazioni Web che offrono scalabilità automatica e disponibilità elevata senza dover gestire l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="445ae-130">[App Services - Web Apps][docs-webapps] hosts web applications allowing auto-scale and high availability without having to manage infrastructure.</span></span>
* <span data-ttu-id="445ae-131">[Azure Active Directory - B2C][docs-b2c] è un servizio di gestione delle identità che consente di personalizzare e controllare il modo in cui i clienti si iscrivono, accedono e gestiscono i profili in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="445ae-131">[Azure Active Directory - B2C][docs-b2c] is an identity management service that enables customization and control over how customers sign up, sign in, and manage their profiles in an application.</span></span>
* <span data-ttu-id="445ae-132">Le [code di archiviazione][docs-storage-queues] archiviano un numero elevato di messaggi in coda ai quali è possibile accedere tramite un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="445ae-132">[Storage Queues][docs-storage-queues] stores large numbers of queue messages that can be accessed by an application.</span></span>
* <span data-ttu-id="445ae-133">Le [funzioni][docs-functions] sono opzioni di calcolo senza server che consentono l'esecuzione di applicazioni su richiesta senza dover gestire l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="445ae-133">[Functions][docs-functions] are serverless compute options that allow applications to run on-demand without having to manage infrastructure.</span></span>
* <span data-ttu-id="445ae-134">[Servizi cognitivi - Analisi del sentiment][docs-sentiment-analysis] usa API di Machine Learning e consente agli sviluppatori di aggiungere facilmente funzionalità intelligenti alle applicazioni, quali il rilevamento di emozioni e video, il riconoscimento facciale, vocale e visivo e la comprensione del parlato e del linguaggio.</span><span class="sxs-lookup"><span data-stu-id="445ae-134">[Cognitive Services - Sentiment Analysis][docs-sentiment-analysis] uses machine learning APIs and enables developers to easily add intelligent features – such as emotion and video detection; facial, speech and vision recognition; and speech and language understanding – into applications.</span></span>
* <span data-ttu-id="445ae-135">[Ricerca di Azure][docs-search] è una soluzione cloud di ricerca distribuita come servizio che offre un'esperienza di ricerca avanzata su contenuti eterogenei e privati nelle applicazioni Web, per dispositivi mobili e aziendali.</span><span class="sxs-lookup"><span data-stu-id="445ae-135">[Azure Search][docs-search] is a search-as-a-service cloud solution that provides a rich search experience over private, heterogenous content in web, mobile, and enterprise applications.</span></span>
* <span data-ttu-id="445ae-136">I [BLOB di archiviazione][docs-storage-blobs] sono ottimizzati per l'archiviazione di grandi quantità di dati non strutturati, ad esempio testo o dati binari.</span><span class="sxs-lookup"><span data-stu-id="445ae-136">[Storage Blobs][docs-storage-blobs] are optimized to store large amounts of unstructured data, such as text or binary data.</span></span>
* <span data-ttu-id="445ae-137">La [cache Redis][docs-redis-cache] migliora le prestazioni e la scalabilità dei sistemi che si affidano fortemente agli archivi dati di back end, copiando temporaneamente i dati a cui si accede di frequente in uno spazio di archiviazione rapida situato vicino all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="445ae-137">[Redis Cache][docs-redis-cache] improves the performance and scalability of systems that rely heavily on backend data-stores by temporarily copying frequently accessed data to fast storage located close to the application.</span></span>
* <span data-ttu-id="445ae-138">Il [database SQL][docs-sql-database] è un servizio gestito di database relazionale per uso generico in Microsoft Azure che supporta strutture come dati relazionali, JSON, dati spaziali e XML.</span><span class="sxs-lookup"><span data-stu-id="445ae-138">[SQL Database][docs-sql-database] is a general-purpose relational database managed service in Microsoft Azure that supports structures such as relational data, JSON, spatial, and XML.</span></span>
* <span data-ttu-id="445ae-139">[Application Insights][docs-application-insights] è progettato per migliorare continuamente le prestazioni e l'usabilità rilevando automaticamente le anomalie delle prestazioni con strumenti di analisi integrati che consentono di rilevare le operazioni eseguite dagli utenti con un'app.</span><span class="sxs-lookup"><span data-stu-id="445ae-139">[Application Insights][docs-application-insights] is designed to help you continuously improve performance and usability by automatically detecting performance anomalies through built-in analytics tools to help understand what users do with an app.</span></span>

### <a name="alternatives"></a><span data-ttu-id="445ae-140">Alternative</span><span class="sxs-lookup"><span data-stu-id="445ae-140">Alternatives</span></span>

<span data-ttu-id="445ae-141">Sono disponibili molte altre tecnologie per compilare un'applicazione rivolta ai clienti focalizzata sull'e-commerce su larga scala.</span><span class="sxs-lookup"><span data-stu-id="445ae-141">Many other technologies are available for building a customer facing application focused on e-commerce at scale.</span></span> <span data-ttu-id="445ae-142">Queste tecnologie coprono sia il front-end dell'applicazione che il livello dati.</span><span class="sxs-lookup"><span data-stu-id="445ae-142">These cover both the front end of the application as well as the data tier.</span></span>

<span data-ttu-id="445ae-143">Altre opzioni per il livello Web e le funzioni includono:</span><span class="sxs-lookup"><span data-stu-id="445ae-143">Other options for the web tier and functions include:</span></span>

* <span data-ttu-id="445ae-144">[Service Fabric][docs-service-fabric]: piattaforma incentrata su componenti distribuiti per i quali sono utili la distribuzione e l'esecuzione in un cluster con un livello elevato di controllo.</span><span class="sxs-lookup"><span data-stu-id="445ae-144">[Service Fabric][docs-service-fabric] - A platform focused around building distributed components that benefit from being deployed and run across a cluster with a high degree of control.</span></span> <span data-ttu-id="445ae-145">È possibile usare Service Fabric anche per l'hosting di contenitori.</span><span class="sxs-lookup"><span data-stu-id="445ae-145">Service Fabric can also be used to host containers.</span></span>
* <span data-ttu-id="445ae-146">[Servizio Kubernetes di Azure][docs-kubernetes-service]: piattaforma per la creazione e la distribuzione di soluzioni basate su contenitori che possono essere usate come un'unica implementazione di un'architettura di microservizi.</span><span class="sxs-lookup"><span data-stu-id="445ae-146">[Azure Kubernetes Service][docs-kubernetes-service] - A platform for building and deploying container based solutions which can be used as one implementation of a microservices architecture.</span></span> <span data-ttu-id="445ae-147">Ciò consente la scalabilità indipendente dei diversi componenti dell'applicazione su richiesta.</span><span class="sxs-lookup"><span data-stu-id="445ae-147">This allows for agility of different components of the application to be able to scale independently on demand.</span></span>
* <span data-ttu-id="445ae-148">[Istanze di contenitore di Azure][docs-container-instances]: modalità di distribuzione ed esecuzione rapida di contenitori con ciclo di vita breve.</span><span class="sxs-lookup"><span data-stu-id="445ae-148">[Azure Container Instances][docs-container-instances] - A way of quickly deploying and running containers with a short lifecycle.</span></span> <span data-ttu-id="445ae-149">Questi contenitori vengono solitamente distribuiti per eseguire un processo di elaborazione rapido, come l'elaborazione di un messaggio o l'esecuzione di un calcolo, quindi vengono immediatamente sottoposti a deprovisioning al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="445ae-149">Containers here are usually deployed to run a quick processing job such as processing a message or performing a calculation and then deprovisioned as soon as they are complete.</span></span>
* <span data-ttu-id="445ae-150">È possibile usare il bus di servizio al posto delle code di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="445ae-150">[Service Bus][service-bus] could be used in place of Storage Queue's.</span></span>

<span data-ttu-id="445ae-151">Altre opzioni per il livello dati includono:</span><span class="sxs-lookup"><span data-stu-id="445ae-151">Other options for the data tier include:</span></span>

* <span data-ttu-id="445ae-152">[Cosmos DB][docs-cosmosdb]: database multimodello di Microsoft distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="445ae-152">[Cosmos DB][docs-cosmosdb] - Microsoft's globally distributed, multi-model database.</span></span> <span data-ttu-id="445ae-153">Offre una piattaforma per eseguire altri modelli di dati come Mongo DB, Cassandra, dati Graph o un semplice archivio tabelle.</span><span class="sxs-lookup"><span data-stu-id="445ae-153">This provides a platform to run other data models such as Mongo DB, Cassandra, Graph data, or simple table storage.</span></span>

## <a name="considerations"></a><span data-ttu-id="445ae-154">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="445ae-154">Considerations</span></span>

### <a name="availability"></a><span data-ttu-id="445ae-155">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="445ae-155">Availability</span></span>

* <span data-ttu-id="445ae-156">Durante la creazione di un'applicazione cloud, valutare la possibilità di sfruttare i [modelli di progettazione tipici per la disponibilità][design-patterns-availability].</span><span class="sxs-lookup"><span data-stu-id="445ae-156">Consider leveraging the [typical design patterns for availability][design-patterns-availability] when building your cloud application.</span></span>
* <span data-ttu-id="445ae-157">Esaminare le considerazioni sulla disponibilità riportate in relazione all'[architettura di riferimento per applicazioni Web del servizio app][app-service-reference-architecture] appropriata.</span><span class="sxs-lookup"><span data-stu-id="445ae-157">Review the availability considerations in the appropriate [App Service web application reference architecture][app-service-reference-architecture]</span></span>
* <span data-ttu-id="445ae-158">Per altre considerazioni sulla disponibilità, vedere l'[elenco di controllo della disponibilità][availability] in Centro architetture.</span><span class="sxs-lookup"><span data-stu-id="445ae-158">For additional considerations concerning availability, please see the [availability checklist][availability] in the architecture center.</span></span>

### <a name="scalability"></a><span data-ttu-id="445ae-159">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="445ae-159">Scalability</span></span>

* <span data-ttu-id="445ae-160">Durante la creazione di un'applicazione cloud, tenere presenti i [modelli di progettazione tipici per la scalabilità][design-patterns-scalability].</span><span class="sxs-lookup"><span data-stu-id="445ae-160">When building a cloud application be aware of the [typical design patterns for scalability][design-patterns-scalability].</span></span>
* <span data-ttu-id="445ae-161">Esaminare le considerazioni sulla scalabilità riportate in relazione all'[architettura di riferimento per applicazioni Web del servizio app][app-service-reference-architecture] appropriata.</span><span class="sxs-lookup"><span data-stu-id="445ae-161">Review the scalability considerations in the appropriate [App Service web application reference architecture][app-service-reference-architecture]</span></span>
* <span data-ttu-id="445ae-162">Per altri argomenti relativi alla scalabilità, vedere l'[elenco di controllo per la scalabilità][scalability] disponibile in Centro architetture.</span><span class="sxs-lookup"><span data-stu-id="445ae-162">For other scalability topics please see the [scalability checklist][scalability] available in the architecture center.</span></span>

### <a name="security"></a><span data-ttu-id="445ae-163">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="445ae-163">Security</span></span>

* <span data-ttu-id="445ae-164">Valutare la possibilità di sfruttare i [modelli di progettazione tipici per la sicurezza][design-patterns-security], quando opportuno.</span><span class="sxs-lookup"><span data-stu-id="445ae-164">Consider leveraging the [typical design patterns for security][design-patterns-security] where appropriate.</span></span>
* <span data-ttu-id="445ae-165">Esaminare le considerazioni sulla sicurezza riportate in relazione all'[architettura di riferimento per applicazioni Web del servizio app][app-service-reference-architecture] appropriata.</span><span class="sxs-lookup"><span data-stu-id="445ae-165">Review the security considerations in the appropriate [App Service web application reference architecture][app-service-reference-architecture].</span></span>
* <span data-ttu-id="445ae-166">Valutare la possibilità di seguire un [ciclo di vita di sviluppo sicuro][secure-development] per consentire agli sviluppatori di creare software più sicuro e di soddisfare requisiti di conformità agli standard di sicurezza riducendo al contempo i costi di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="445ae-166">Consider following a [secure development lifecycle][secure-development] process to help developers build more secure software and address security compliance requirements while reducing development cost.</span></span>
* <span data-ttu-id="445ae-167">Esaminare l'architettura di progetto per la [conformità PCI DSS di Azure][pci-dss-blueprint].</span><span class="sxs-lookup"><span data-stu-id="445ae-167">Review the blueprint architecture for [Azure PCI DSS compliance][pci-dss-blueprint].</span></span>

### <a name="resiliency"></a><span data-ttu-id="445ae-168">Resilienza</span><span class="sxs-lookup"><span data-stu-id="445ae-168">Resiliency</span></span>

* <span data-ttu-id="445ae-169">Valutare la possibilità di sfruttare il [modello a interruttore][circuit-breaker] per offrire una gestione degli errori senza interruzioni se una parte dell'applicazione non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="445ae-169">Consider leveraging the [circuit breaker pattern][circuit-breaker] to provide graceful error handling should one part of the application not be available.</span></span>
* <span data-ttu-id="445ae-170">Esaminare i [modelli di progettazione tipici per la resilienza][design-patterns-resiliency] e valutare la possibilità di implementarli, quando opportuno.</span><span class="sxs-lookup"><span data-stu-id="445ae-170">Review the [typical design patterns for resiliency][design-patterns-resiliency] and consider implementing these where appropriate.</span></span>
* <span data-ttu-id="445ae-171">In Centro architetture sono disponibili diverse [procedure consigliate per la resilienza per il servizio app][resiliency-app-service].</span><span class="sxs-lookup"><span data-stu-id="445ae-171">You can find a number of [resiliency recommended practices for App Service][resiliency-app-service] on the architecture center.</span></span>
* <span data-ttu-id="445ae-172">Valutare la possibilità di usare la [replica geografica attiva][sql-geo-replication] per il livello dati e l'archiviazione [con ridondanza geografica][storage-geo-redudancy] per le immagini e le code.</span><span class="sxs-lookup"><span data-stu-id="445ae-172">Consider using active [geo-replication][sql-geo-replication] for the data tier and [geo-redundant][storage-geo-redudancy] storage for images and queues.</span></span>
* <span data-ttu-id="445ae-173">Per una discussione più approfondita sulla [resilienza][resiliency], vedere l'articolo corrispondente in Centro architetture.</span><span class="sxs-lookup"><span data-stu-id="445ae-173">For a deeper discussion on [resiliency][resiliency] please see the relevant article in the architecture center.</span></span>

## <a name="deploy-the-scenario"></a><span data-ttu-id="445ae-174">Distribuire lo scenario</span><span class="sxs-lookup"><span data-stu-id="445ae-174">Deploy the scenario</span></span>

<span data-ttu-id="445ae-175">Per distribuire questo scenario, è possibile seguire l'[esercitazione dettagliata][end-to-end-walkthrough] che illustra come distribuire manualmente ogni componente.</span><span class="sxs-lookup"><span data-stu-id="445ae-175">To deploy this scenario, you can follow this [step-by-step tutorial][end-to-end-walkthrough] demonstrating how to manually deploy each component.</span></span> <span data-ttu-id="445ae-176">Questa esercitazione fornisce anche un'applicazione .NET di esempio che esegue una semplice applicazione per l'acquisto di biglietti.</span><span class="sxs-lookup"><span data-stu-id="445ae-176">This tutorial also provides a .NET sample application that runs a simple ticket purchasing application.</span></span> <span data-ttu-id="445ae-177">È anche disponibile un modello di Azure Resource Manager per automatizzare la distribuzione della maggior parte delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="445ae-177">Additionally, there is an ARM template to automate the deployment of most of the Azure resources.</span></span>

## <a name="pricing"></a><span data-ttu-id="445ae-178">Prezzi</span><span class="sxs-lookup"><span data-stu-id="445ae-178">Pricing</span></span>

<span data-ttu-id="445ae-179">Esaminare il costo di esecuzione dello scenario. Nel calcolatore dei costi sono preconfigurati tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="445ae-179">Explore the cost of running this scenario, all of the services are pre-configured in the cost calculator.</span></span> <span data-ttu-id="445ae-180">Per verificare la variazione dei prezzi per un determinato caso d'uso, modificare le variabili appropriate in base al traffico previsto.</span><span class="sxs-lookup"><span data-stu-id="445ae-180">To see how the pricing would change for your particular use case change the appropriate variables to match your expected traffic.</span></span>

<span data-ttu-id="445ae-181">Sono stati definiti tre profili di costo di esempio in base alla quantità di traffico prevista.</span><span class="sxs-lookup"><span data-stu-id="445ae-181">We have provided three sample cost profiles based on amount of traffic you expect to get:</span></span>

* <span data-ttu-id="445ae-182">[Small][small-pricing]: rappresenta i componenti necessari per un'istanza di livello produzione minima.</span><span class="sxs-lookup"><span data-stu-id="445ae-182">[Small][small-pricing]: This represents the components necessary to build the out for a minimum production level instance.</span></span> <span data-ttu-id="445ae-183">In questo caso si ipotizza un numero limitato di utenti, ovvero solo alcune migliaia al mese.</span><span class="sxs-lookup"><span data-stu-id="445ae-183">Here we are assuming a small amount of users, numbering only in a few thousand per month.</span></span> <span data-ttu-id="445ae-184">L'app usa una singola istanza di un'app Web standard, sufficiente per abilitare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="445ae-184">The app is using a single instance of a standard web app which will be enough to enable autoscaling.</span></span> <span data-ttu-id="445ae-185">Ognuno degli altri componenti viene ridimensionato a un livello Basic che consente un costo minimo, garantendo comunque un supporto con contratto di servizio e capacità sufficiente per gestire un carico di lavoro a livello di produzione.</span><span class="sxs-lookup"><span data-stu-id="445ae-185">Each of the other components are scaled to a basic tier which will allow for a minimum amount of cost but still ensure that there is SLA support and enough capacity to handle a production level workload.</span></span>
* <span data-ttu-id="445ae-186">[Medium][medium-pricing]: rappresenta i componenti indicativi di una distribuzione di medie dimensioni.</span><span class="sxs-lookup"><span data-stu-id="445ae-186">[Medium][medium-pricing]: This represents the components indicative of a moderate size deployment.</span></span> <span data-ttu-id="445ae-187">In questo caso si stimano circa 100.000 utenti che usano il sistema nel corso di un mese.</span><span class="sxs-lookup"><span data-stu-id="445ae-187">Here we estimate approximately 100,000 users using the system over the course of a month.</span></span> <span data-ttu-id="445ae-188">Il traffico previsto viene gestito in una singola istanza del servizio app con un livello Standard moderato.</span><span class="sxs-lookup"><span data-stu-id="445ae-188">The expected traffic is handled in a single app service instance with a moderate standard tier.</span></span> <span data-ttu-id="445ae-189">Al calcolatore vengono anche aggiunti livelli moderati di servizi cognitivi e di ricerca.</span><span class="sxs-lookup"><span data-stu-id="445ae-189">Additionally, moderate tiers of cognitive and search services are added to the calculator.</span></span>
* <span data-ttu-id="445ae-190">[Large][large-pricing]: rappresenta un'applicazione su larga scala, nell'ordine di milioni di utenti al mese, con il trasferimento di terabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="445ae-190">[Large][large-pricing]: This represents an application meant for high scale, at the order of millions of users per month moving terabytes of data.</span></span> <span data-ttu-id="445ae-191">Questo livello di utilizzo richiede app Web di livello Premium con prestazioni elevate, distribuite in più aree e gestite da Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="445ae-191">At this level of usage high performance, premium tier web apps deployed in multiple regions fronted by traffic manager is required.</span></span> <span data-ttu-id="445ae-192">I dati sono costituiti da archivi, database e rete CDN, configurati per terabyte di dati.</span><span class="sxs-lookup"><span data-stu-id="445ae-192">Data consists of the following: storage, databases, and CDN, are configured for terabytes of data.</span></span>

## <a name="related-resources"></a><span data-ttu-id="445ae-193">Risorse correlate</span><span class="sxs-lookup"><span data-stu-id="445ae-193">Related Resources</span></span>

* <span data-ttu-id="445ae-194">[Architettura di riferimento per applicazioni Web per più aree][multi-region-web-app]</span><span class="sxs-lookup"><span data-stu-id="445ae-194">[Reference Architecture for Multi-Region Web Application][multi-region-web-app]</span></span>
* <span data-ttu-id="445ae-195">[Esempio di riferimento eShopOnContainers][microservices-ecommerce]</span><span class="sxs-lookup"><span data-stu-id="445ae-195">[eShop on Containers Reference Example][microservices-ecommerce]</span></span>

<!-- links -->
[small-pricing]: https://azure.com/e/90fbb6a661a04888a57322985f9b34ac
[medium-pricing]: https://azure.com/e/38d5d387e3234537b6859660db1c9973
[large-pricing]: https://azure.com/e/f07f99b6c3134803a14c9b43fcba3e2f
[app-service-reference-architecture]: /azure/architecture/reference-architectures/app-service-web-app/
[architecture-diagram]: ./media/architecture-diagram-ecommerce-solution.png
[availability]: /azure/architecture/checklist/availability
[circuit-breaker]: /azure/architecture/patterns/circuit-breaker
[design-patterns-availability]: /azure/architecture/patterns/category/availability
[design-patterns-resiliency]: /azure/architecture/patterns/category/resiliency
[design-patterns-scalability]: /azure/architecture/patterns/category/performance-scalability
[design-patterns-security]: /azure/architecture/patterns/category/security
[docs-application-insights]: /azure/application-insights/app-insights-overview
[docs-b2c]: /azure/active-directory-b2c/active-directory-b2c-overview
[docs-cdn]: /azure/cdn/cdn-overview
[docs-container-instances]: /azure/container-instances/
[docs-kubernetes-service]: /azure/aks/
[docs-cosmosdb]: /azure/cosmos-db/
[docs-functions]: /azure/azure-functions/functions-overview
[docs-redis-cache]: /azure/redis-cache/cache-overview
[docs-search]: /azure/search/search-what-is-azure-search
[docs-service-fabric]: /azure/service-fabric/
[docs-sentiment-analysis]: /azure/cognitive-services/welcome
[docs-sql-database]: /azure/sql-database/sql-database-technical-overview
[docs-storage-blobs]: /azure/storage/blobs/storage-blobs-introduction
[docs-storage-queues]: /azure/storage/queues/storage-queues-introduction
[docs-traffic-manager]: /azure/traffic-manager/traffic-manager-overview
[docs-webapps]: /azure/app-service/app-service-web-overview
[end-to-end-walkthrough]: https://github.com/Azure/fta-customerfacingapps/tree/master/ecommerce/articles
[microservices-ecommerce]: https://github.com/dotnet-architecture/eShopOnContainers
[multi-region-web-app]: /azure/architecture/reference-architectures/app-service-web-app/multi-region
[pci-dss-blueprint]: /azure/security/blueprints/payment-processing-blueprint
[resiliency-app-service]: /azure/architecture/checklist/resiliency-per-service#app-service
[resiliency]: /azure/architecture/checklist/resiliency
[scalability]: /azure/architecture/checklist/scalability
[secure-development]: https://www.microsoft.com/en-us/SDL/process/design.aspx
[sql-geo-replication]: /azure/sql-database/sql-database-geo-replication-overview
[storage-geo-redudancy]: /azure/storage/common/storage-redundancy-grs