---
title: Funzioni di Azure per l'elaborazione degli eventi senza server
description: Architettura di riferimento che mostra l'elaborazione e l'inserimento di eventi senza server
author: MikeWasson
ms.date: 10/16/2018
ms.openlocfilehash: 2bb7600fbed95e4b9368cf342c0bc6a75c5f8755
ms.sourcegitcommit: 113a7248b9793c670b0f2d4278d30ad8616abe6c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49349939"
---
# <a name="serverless-event-processing-using-azure-functions"></a><span data-ttu-id="29c3d-103">Funzioni di Azure per l'elaborazione degli eventi senza server</span><span class="sxs-lookup"><span data-stu-id="29c3d-103">Serverless event processing using Azure Functions</span></span>

<span data-ttu-id="29c3d-104">Questa architettura di riferimento illustra un'architettura senza server e basata su eventi, che inserisce un flusso di dati, li elabora e scrive i risultati in un database back-end.</span><span class="sxs-lookup"><span data-stu-id="29c3d-104">This reference architecture shows a serverless, event-driven architecture that ingests a stream of data, processes the data, and writes the results to a back-end database.</span></span> <span data-ttu-id="29c3d-105">Un'implementazione di riferimento per questa architettura è disponibile in [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="29c3d-105">A reference implementation for this architecture is available on [GitHub][github].</span></span>

![](./_images/serverless-event-processing.png)

## <a name="architecture"></a><span data-ttu-id="29c3d-106">Architettura</span><span class="sxs-lookup"><span data-stu-id="29c3d-106">Architecture</span></span>

<span data-ttu-id="29c3d-107">**Hub eventi** inserisce il flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="29c3d-107">**Event Hubs** ingests the data stream.</span></span> <span data-ttu-id="29c3d-108">[Hub eventi][eh] è progettato per scenari di flusso di dati con velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="29c3d-108">[Event Hubs][eh] is designed for high-throughput data streaming scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="29c3d-109">Per gli scenari IoT, è consigliabile usare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="29c3d-109">For IoT scenarios, we recommend IoT Hub.</span></span> <span data-ttu-id="29c3d-110">L'hub IoT ha un endpoint predefinito che è compatibile con l'API di Hub eventi di Azure, pertanto è possibile usare uno dei due servizi nell'architettura senza apportare modifiche rilevanti nell'elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="29c3d-110">IoT Hub has a built-in endpoint that’s compatible with the Azure Event Hubs API, so you can use either service in this architecture with no major changes in the backend processing.</span></span> <span data-ttu-id="29c3d-111">Per informazioni, vedere [Connessione di dispositivi IoT ad Azure: hub IoT e hub eventi][iot].</span><span class="sxs-lookup"><span data-stu-id="29c3d-111">For more information, see [Connecting IoT Devices to Azure: IoT Hub and Event Hubs][iot].</span></span>

<span data-ttu-id="29c3d-112">**App per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-112">**Function App**.</span></span> <span data-ttu-id="29c3d-113">[Funzioni di Azure][functions] è un'opzione di calcolo senza server.</span><span class="sxs-lookup"><span data-stu-id="29c3d-113">[Azure Functions][functions] is a serverless compute option.</span></span> <span data-ttu-id="29c3d-114">Usa un modello basato su eventi, in cui un frammento di codice, vale a dire una "funzione", viene richiamato da un trigger.</span><span class="sxs-lookup"><span data-stu-id="29c3d-114">It uses an event-driven model, where a piece of code (a “function”) is invoked by a trigger.</span></span> <span data-ttu-id="29c3d-115">In questa architettura, quando gli eventi arrivano a Hub eventi, attivano una funzione che elabora gli eventi e scrive i risultati nell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-115">In this architecture, when events arrive at Event Hubs, they trigger a function that processes the events and writes the results to storage.</span></span>

<span data-ttu-id="29c3d-116">Le app per le funzioni sono adatte per l'elaborazione di singoli record da Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="29c3d-116">Function Apps are suitable for processing individual records from Event Hubs.</span></span> <span data-ttu-id="29c3d-117">Per gli scenari di elaborazione del flusso più complessi, prendere in considerazione Apache Spark con Azure Databricks, oppure Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="29c3d-117">For more complex stream processing scenarios, consider Apache Spark using Azure Databricks, or Azure Stream Analytics.</span></span>

<span data-ttu-id="29c3d-118">**Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-118">**Cosmos DB**.</span></span> <span data-ttu-id="29c3d-119">[Cosmos DB][cosmosdb] è un servizio database multimodello.</span><span class="sxs-lookup"><span data-stu-id="29c3d-119">[Cosmos DB][cosmosdb] is a multi-model database service.</span></span> <span data-ttu-id="29c3d-120">Per questo scenario, la funzione di elaborazione di eventi archivia i record JSON, usando l'[API SQL][cosmosdb-sql] di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29c3d-120">For this scenario, the event-processing function stores JSON records, using the Cosmos DB [SQL API][cosmosdb-sql].</span></span>

<span data-ttu-id="29c3d-121">**Archiviazione code**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-121">**Queue storage**.</span></span> <span data-ttu-id="29c3d-122">[Archiviazione code][queue] viene usato per i messaggi non recapitabili.</span><span class="sxs-lookup"><span data-stu-id="29c3d-122">[Queue storage][queue] is used for dead letter messages.</span></span> <span data-ttu-id="29c3d-123">Se si verifica un errore durante l'elaborazione di un evento, la funzione archivia i dati dell'evento in una coda di messaggi non recapitabili per elaborali in seguito.</span><span class="sxs-lookup"><span data-stu-id="29c3d-123">If an error occurs while processing an event, the function stores the event data in a dead letter queue for later processing.</span></span> <span data-ttu-id="29c3d-124">Per altre informazioni, vedere [Resiliency Considerations](#resiliency-considerations) (Considerazioni sulla resilienza).</span><span class="sxs-lookup"><span data-stu-id="29c3d-124">For more information, see [Resiliency Considerations](#resiliency-considerations).</span></span>

<span data-ttu-id="29c3d-125">**Monitoraggio di Azure**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-125">**Azure Monitor**.</span></span> <span data-ttu-id="29c3d-126">[Monitoraggio][monitor] raccoglie le metriche relative alle prestazioni dei servizi di Azure distribuiti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-126">[Monitor][monitor] collects performance metrics about the Azure services deployed in the solution.</span></span> <span data-ttu-id="29c3d-127">La visualizzazione delle metriche in una dashboard consente di ottenere visibilità sull'integrità della soluzione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-127">By visualizing these in a dashboard, you can get visibility  into the health of the solution.</span></span>

<span data-ttu-id="29c3d-128">**Azure Pipelines**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-128">**Azure Pipelines**.</span></span> <span data-ttu-id="29c3d-129">[Pipelines][pipelines] è un servizio di integrazione continua, ovvero CI, e recapito continuo, ovvero CD, che compila, verifica e distribuisce l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-129">[Pipelines][pipelines] is a continuous integration (CI) and continuous delivery (CD) service that builds, tests, and deploys the application.</span></span>

## <a name="scalability-considerations"></a><span data-ttu-id="29c3d-130">Considerazioni sulla scalabilità</span><span class="sxs-lookup"><span data-stu-id="29c3d-130">Scalability considerations</span></span>

### <a name="event-hubs"></a><span data-ttu-id="29c3d-131">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="29c3d-131">Event Hubs</span></span>

<span data-ttu-id="29c3d-132">La capacità di elaborazione di Hub eventi viene misurata in [unità elaborate][eh-throughput].</span><span class="sxs-lookup"><span data-stu-id="29c3d-132">The throughput capacity of Event Hubs is measured in [throughput units][eh-throughput].</span></span> <span data-ttu-id="29c3d-133">È possibile ridimensionare automaticamente un hub eventi abilitando l'[aumento automatico][eh-autoscale], che ridimensiona automaticamente le unità elaborate in base al traffico, fino a un limite massimo configurato.</span><span class="sxs-lookup"><span data-stu-id="29c3d-133">You can autoscale an event hub by enabling [auto-inflate][eh-autoscale], which automatically scales the throughput units based on traffic, up to a configured maximum.</span></span>

<span data-ttu-id="29c3d-134">Il [trigger di Hub eventi][eh-trigger] nell'app per le funzioni viene ridimensionato in base al numero di partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="29c3d-134">The [Event Hub trigger][eh-trigger] in the function app scales according to the number of partitions in the event hub.</span></span> <span data-ttu-id="29c3d-135">A ogni partizione viene assegnata un'istanza di funzione alla volta.</span><span class="sxs-lookup"><span data-stu-id="29c3d-135">Each partition is assigned one function instance at a time.</span></span> <span data-ttu-id="29c3d-136">Per ottimizzare la velocità effettiva, ricevere gli eventi in batch, anziché uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="29c3d-136">To maximize throughput, receive the events in a batch, instead of one at a time.</span></span>

### <a name="cosmos-db"></a><span data-ttu-id="29c3d-137">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29c3d-137">Cosmos DB</span></span>

<span data-ttu-id="29c3d-138">La capacità di elaborazione per Cosmos DB viene misurata in [unità richiesta][ru] (UR).</span><span class="sxs-lookup"><span data-stu-id="29c3d-138">Throughput capacity for Cosmos DB is measured in [Request Units][ru] (RU).</span></span> <span data-ttu-id="29c3d-139">Per ridimensionare un contenitore Cosmos DB fino a un valore superiore a 10.000 UR, è necessario specificare una [chiave di partizione][partition-key] quando si crea il contenitore e includere la chiave di partizione in ogni documento creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="29c3d-139">In order to scale a Cosmos DB container past 10,000 RU, you must specify a [partition key][partition-key] when you create the container, and include the partition key in every document that you create.</span></span>

<span data-ttu-id="29c3d-140">Ecco alcune caratteristiche di una chiave di partizione efficace:</span><span class="sxs-lookup"><span data-stu-id="29c3d-140">Here are some characteristics of a good partition key:</span></span>

- <span data-ttu-id="29c3d-141">Lo spazio dei valori della chiave è grande.</span><span class="sxs-lookup"><span data-stu-id="29c3d-141">The key value space is large.</span></span> 
- <span data-ttu-id="29c3d-142">Si verificherà una distribuzione uniforme delle operazioni di lettura/scrittura per ogni valore della chiave, evitando le chiavi usate di frequente.</span><span class="sxs-lookup"><span data-stu-id="29c3d-142">There will be an even distribution of reads/writes per key value, avoiding hot keys.</span></span>
- <span data-ttu-id="29c3d-143">Il numero massimo di dati archiviati per ogni singolo valore della chiave non supererà le dimensioni massime di una partizione fisica (10 GB).</span><span class="sxs-lookup"><span data-stu-id="29c3d-143">The maximum data stored for any single key value will not exceed the maximum physical partition size (10 GB).</span></span> 
- <span data-ttu-id="29c3d-144">La chiave di partizione per un documento non cambierà.</span><span class="sxs-lookup"><span data-stu-id="29c3d-144">The partition key for a document won't change.</span></span> <span data-ttu-id="29c3d-145">Non è possibile aggiornare la chiave di partizione su un documento esistente.</span><span class="sxs-lookup"><span data-stu-id="29c3d-145">You can't update the partition key on an existing document.</span></span> 

<span data-ttu-id="29c3d-146">Nello scenario per questa architettura di riferimento la funzione archivia esattamente un documento per ogni dispositivo che invia dati.</span><span class="sxs-lookup"><span data-stu-id="29c3d-146">In the scenario for this reference architecture, the function stores exactly one document per device that is sending data.</span></span> <span data-ttu-id="29c3d-147">La funzione aggiorna continuamente i documenti con lo stato del dispositivo più recente, mediante un'operazione upsert.</span><span class="sxs-lookup"><span data-stu-id="29c3d-147">The function continually updates the documents with latest device status, using an upsert operation.</span></span> <span data-ttu-id="29c3d-148">L'ID dispositivo rappresenta una chiave di partizione efficace per questo scenario, perché le scritture verranno distribuite in modo uniforme tra le chiavi e le dimensioni di ogni partizione verranno rigorosamente limitate, essendo presente un solo documento per ogni valore di chiave.</span><span class="sxs-lookup"><span data-stu-id="29c3d-148">Device ID is a good partition key for this scenario, because writes will be evenly distributed across the keys, and the size of each partition will be strictly bounded, because there is a single document for each key value.</span></span> <span data-ttu-id="29c3d-149">Per altre informazioni sulle chiavi di partizione, vedere [Partizionamento e ridimensionamento in Azure Cosmos DB][cosmosdb-scale].</span><span class="sxs-lookup"><span data-stu-id="29c3d-149">For more information about partition keys, see [Partition and scale in Azure Cosmos DB][cosmosdb-scale].</span></span>

## <a name="resiliency-considerations"></a><span data-ttu-id="29c3d-150">Considerazioni sulla resilienza</span><span class="sxs-lookup"><span data-stu-id="29c3d-150">Resiliency considerations</span></span>

<span data-ttu-id="29c3d-151">Quando si usa il trigger di Hub eventi con Funzioni, intercettare le eccezioni all'interno del ciclo di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-151">When using the Event Hubs trigger with Functions, catch exceptions within your processing loop.</span></span> <span data-ttu-id="29c3d-152">Se si verifica un'eccezione non gestita, il runtime di Funzioni non ripete i messaggi.</span><span class="sxs-lookup"><span data-stu-id="29c3d-152">If an unhandled exception occurs, the Functions runtime does not retry the messages.</span></span> <span data-ttu-id="29c3d-153">Se non è possibile elaborare un messaggio, inserire il messaggio in una coda di messaggi non recapitabili.</span><span class="sxs-lookup"><span data-stu-id="29c3d-153">If a message cannot be processed, put the message into a dead letter queue.</span></span> <span data-ttu-id="29c3d-154">Usare un processo fuori banda per esaminare i messaggi e determinare l'azione correttiva.</span><span class="sxs-lookup"><span data-stu-id="29c3d-154">Use an out-of-band process to examine the messages and determine corrective action.</span></span> 

<span data-ttu-id="29c3d-155">Il codice seguente illustra in che modo la funzione di inserimento intercetta le eccezioni e inserisce i messaggi non elaborati in una coda di messaggi non recapitabili.</span><span class="sxs-lookup"><span data-stu-id="29c3d-155">The following code shows how the ingestion function catches exceptions and puts unprocessed messages onto a dead letter queue.</span></span>

```csharp
[FunctionName("RawTelemetryFunction")]
[StorageAccount("DeadLetterStorage")]
public static async Task RunAsync(
    [EventHubTrigger("%EventHubName%", Connection = "EventHubConnection", ConsumerGroup ="%EventHubConsumerGroup%")]EventData[] messages,
    [Queue("deadletterqueue")] IAsyncCollector<DeadLetterMessage> deadLetterMessages,
    ILogger logger)
{
    foreach (var message in messages)
    {
        DeviceState deviceState = null;

        try
        {
            deviceState = telemetryProcessor.Deserialize(message.Body.Array, logger);
        }
        catch (Exception ex)
        {
            logger.LogError(ex, "Error deserializing message", message.SystemProperties.PartitionKey, message.SystemProperties.SequenceNumber);
            await deadLetterMessages.AddAsync(new DeadLetterMessage { Issue = ex.Message, EventData = message });
        }

        try
        {
            await stateChangeProcessor.UpdateState(deviceState, logger);
        }
        catch (Exception ex)
        {
            logger.LogError(ex, "Error updating status document", deviceState);
            await deadLetterMessages.AddAsync(new DeadLetterMessage { Issue = ex.Message, EventData = message, DeviceState = deviceState });
        }
    }
}
```

<span data-ttu-id="29c3d-156">Si noti che la funzione usa l'[associazione di output di archiviazione code][queue-binding] per inserire elementi nella coda.</span><span class="sxs-lookup"><span data-stu-id="29c3d-156">Notice that the function uses the [Queue storage output binding][queue-binding] to put items in the queue.</span></span>

<span data-ttu-id="29c3d-157">Il codice illustrato sopra registra anche le eccezioni per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="29c3d-157">The code shown above also logs exceptions to Application Insights.</span></span> <span data-ttu-id="29c3d-158">È possibile usare il numero di sequenza e la chiave di partizione per correlare i messaggi non recapitabili con le eccezioni nei log.</span><span class="sxs-lookup"><span data-stu-id="29c3d-158">You can use the partition key and sequence number to correlate dead letter messages with the exceptions in the logs.</span></span> 

<span data-ttu-id="29c3d-159">I messaggi nella coda di messaggi non recapitabili avranno sufficienti informazioni in modo da poter comprendere il contesto dell'errore.</span><span class="sxs-lookup"><span data-stu-id="29c3d-159">Messages in the dead letter queue should have enough information so that you can understand the context of error.</span></span> <span data-ttu-id="29c3d-160">In questo esempio, la classe `DeadLetterMessage` contiene il messaggio di eccezione, i dati dell'evento originale e il messaggio di evento deserializzato, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="29c3d-160">In this example, the `DeadLetterMessage` class contains the exception message, the original event data, and the deserialized event message (if available).</span></span> 

```csharp
public class DeadLetterMessage
{
    public string Issue { get; set; }
    public EventData EventData { get; set; }
    public DeviceState DeviceState { get; set; }
}
```

<span data-ttu-id="29c3d-161">Usare [Monitoraggio di Azure][monitor] per monitorare l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="29c3d-161">Use [Azure Monitor][monitor] to monitor the event hub.</span></span> <span data-ttu-id="29c3d-162">Se viene visualizzato un input ma non un output, significa che i messaggi non vengono elaborati.</span><span class="sxs-lookup"><span data-stu-id="29c3d-162">If you see there is input but no output, it means that messages are not being processed.</span></span> <span data-ttu-id="29c3d-163">In tal caso, passare a [Log Analytics][log-analytics] e cercare le eccezioni o altri errori.</span><span class="sxs-lookup"><span data-stu-id="29c3d-163">In that case, go into [Log Analytics][log-analytics] and look for exceptions or other errors.</span></span>

## <a name="disaster-recovery-considerations"></a><span data-ttu-id="29c3d-164">Considerazioni sul ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="29c3d-164">Disaster recovery considerations</span></span>

<span data-ttu-id="29c3d-165">La distribuzione illustrata di seguito si trova in una sola area di Azure.</span><span class="sxs-lookup"><span data-stu-id="29c3d-165">The deployment shown here resides in a single Azure region.</span></span> <span data-ttu-id="29c3d-166">Per un approccio più resiliente al ripristino di emergenza, sfruttare le funzionalità di distribuzione a livello geografico nei vari servizi:</span><span class="sxs-lookup"><span data-stu-id="29c3d-166">For a more resilient approach to disaster-recovery, take advantage of geo-distribution features in the various services:</span></span>

- <span data-ttu-id="29c3d-167">**Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-167">**Event Hubs**.</span></span> <span data-ttu-id="29c3d-168">Creare due spazi dei nomi di Hub eventi, uno spazio dei nomi primario (attivo) e un spazio dei nomi secondario (passivo).</span><span class="sxs-lookup"><span data-stu-id="29c3d-168">Create two Event Hubs namespaces, a primary (active) namespace and a secondary (passive) namespace.</span></span> <span data-ttu-id="29c3d-169">I messaggi vengono indirizzati automaticamente allo spazio dei nomi attivo a meno che non si esegua il failover nello spazio dei nomi secondario.</span><span class="sxs-lookup"><span data-stu-id="29c3d-169">Messages are automatically routed to the active namespace unless you fail over to the secondary namespace.</span></span> <span data-ttu-id="29c3d-170">Per altre informazioni, vedere [Ripristino di emergenza geografico nel servizio Hub eventi di Azure][eh-dr].</span><span class="sxs-lookup"><span data-stu-id="29c3d-170">For more information, see [Azure Event Hubs Geo-disaster recovery][eh-dr].</span></span>

- <span data-ttu-id="29c3d-171">**App per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-171">**Function App**.</span></span> <span data-ttu-id="29c3d-172">Distribuire una seconda app per le funzioni che è in attesa di leggere lo spazio dei nomi secondario di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="29c3d-172">Deploy a second function app that is waiting to read from the secondary Event Hubs namespace.</span></span> <span data-ttu-id="29c3d-173">Questa funzione scrive in un account di archiviazione secondario per la coda di messaggi non recapitabili.</span><span class="sxs-lookup"><span data-stu-id="29c3d-173">This function writes to a secondary storage account for dead letter queue.</span></span>

- <span data-ttu-id="29c3d-174">**Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-174">**Cosmos DB**.</span></span> <span data-ttu-id="29c3d-175">Cosmos DB supporta [più aree master][cosmosdb-geo], che consentono di effettuare operazioni di scrittura in tutte le aree aggiunte al proprio account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29c3d-175">Cosmos DB supports [multiple master regions][cosmosdb-geo], which enables writes to any region that you add to your Cosmos DB account.</span></span> <span data-ttu-id="29c3d-176">Se non si abilita multimaster, è comunque possibile eseguire il failover dell'area di scrittura primaria.</span><span class="sxs-lookup"><span data-stu-id="29c3d-176">If you don’t enable multi-master, you can still fail over the primary write region.</span></span> <span data-ttu-id="29c3d-177">Gli SDK del client Cosmos DB e le associazioni di Funzioni di Azure gestiscono automaticamente il failover, quindi non è necessario aggiornare le impostazioni di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29c3d-177">The Cosmos DB client SDKs and the Azure Function bindings automatically handle the failover, so you don’t need to update any application configuration settings.</span></span>

- <span data-ttu-id="29c3d-178">**Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="29c3d-178">**Azure Storage**.</span></span> <span data-ttu-id="29c3d-179">Usare lo spazio di archiviazione [RA-GRS][ra-grs] per la coda di messaggi non recapitabili.</span><span class="sxs-lookup"><span data-stu-id="29c3d-179">Use [RA-GRS][ra-grs] storage for the dead letter queue.</span></span> <span data-ttu-id="29c3d-180">Verrà creata una replica di sola lettura in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="29c3d-180">This creates a read-only replica in another region.</span></span> <span data-ttu-id="29c3d-181">Se l'area primaria diventa non disponibile, è possibile leggere gli elementi attualmente presenti nella coda.</span><span class="sxs-lookup"><span data-stu-id="29c3d-181">If the primary region becomes unavailable, you can read the items currently in the queue.</span></span> <span data-ttu-id="29c3d-182">In aggiunta eseguire il provisioning di un altro account di archiviazione nella regione secondaria in cui la funzione può scrivere dopo un failover.</span><span class="sxs-lookup"><span data-stu-id="29c3d-182">In addition, provision another storage account in the secondary region that the function can write to after a fail-over.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="29c3d-183">Distribuire la soluzione</span><span class="sxs-lookup"><span data-stu-id="29c3d-183">Deploy the solution</span></span>

<span data-ttu-id="29c3d-184">Per distribuire questa architettura di riferimento, consultare il [file leggimi di GitHub][readme].</span><span class="sxs-lookup"><span data-stu-id="29c3d-184">To deploy this reference architecture, view the [GitHub readme][readme].</span></span> 

<!-- links -->

[cosmosdb]: /azure/cosmos-db/introduction
[cosmosdb-geo]: /azure/cosmos-db/distribute-data-globally
[cosmosdb-scale]: /azure/cosmos-db/partition-data
[cosmosdb-sql]: /azure/cosmos-db/sql-api-introduction
[eh]: /azure/event-hubs/
[eh-autoscale]: /azure/event-hubs/event-hubs-auto-inflate
[eh-dr]: /azure/event-hubs/event-hubs-geo-dr
[eh-throughput]: /azure/event-hubs/event-hubs-features#throughput-units
[eh-trigger]: /azure/azure-functions/functions-bindings-event-hubs
[functions]: /azure/azure-functions/functions-overview
[iot]: /azure/iot-hub/iot-hub-compare-event-hubs
[log-analytics]: /azure/log-analytics/log-analytics-queries
[monitor]: /azure/azure-monitor/overview
[partition-key]: /azure/cosmos-db/partition-data
[pipelines]: /azure/devops/pipelines/index
[queue]: /azure/storage/queues/storage-queues-introduction
[queue-binding]: /azure/azure-functions/functions-bindings-storage-queue#output
[ra-grs]: /azure/storage/common/storage-redundancy-grs
[ru]: /azure/cosmos-db/request-units

[github]: https://github.com/mspnp/serverless-reference-implementation
[readme]: https://github.com/mspnp/serverless-reference-implementation/blob/master/README.md