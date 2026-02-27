# Microsoft Fabric Fabric Analyst in a Day-Lab 1

![](../media/Lab-01/main1.png)

# Sommario
- Struttura del documento
- Scenario/Esposizione del problema	
- Panoramica del report di Power BI Desktop	
  - Attività 1: Impostazione di Power BI Desktop nell'ambiente lab	
  - Attività 2: Analisi del report di Power BI Desktop	
  - Attività 3: Analisi delle query in Power Query	
- Riferimenti	

# Struttura del documento

Il lab include i passaggi che l'utente deve seguire con gli screenshot
associati che forniscono un aiuto visivo. In ogni screenshot vi sono
sezioni evidenziate con riquadri arancioni che indicano le aree su
cui l'utente deve concentrarsi.

>**Nota:** alcuni screenshot potrebbero non essere aggiornati a causa dei
continui aggiornamenti del prodotto.

# Scenario/Esposizione del problema

Fabrikam, Inc. è un distributore di oggettistica all'ingrosso. Poiché
Fabrikam è un grossista, i suoi clienti sono soprattutto aziende che
rivendono ai consumatori. Fabrikam vende a rivenditori al dettaglio in
tutti gli Stati Uniti, inclusi negozi specializzati, supermercati,
negozi di informatica e di souvenir per turisti. Fabrikam vende anche ad
altri grossisti attraverso una rete di agenti che promuovono i prodotti
per conto di Fabrikam. Sebbene tutti i clienti di Fabrikam abbiano sede
negli Stati Uniti, l'azienda desidera espandersi in altri paesi/aree
geografiche.

In qualità di analisti dei dati del team di vendita, si raccolgono,
puliscono e interpretano set di dati per risolvere i problemi aziendali.
Si compongono anche visualizzazioni come grafici e diagrammi,
si scrivono report e li presentano ai decision-maker
dell'organizzazione.

Per ottenere informazioni utili, si estraggono, puliscono e organizzano
insieme dati provenienti da più sistemi. Si ottengono dati dalle
seguenti origini:

- **Dati vendita:** provengono dal sistema ERP e sono archiviati in un
  database ADLS Gen2. Vengono aggiornati alle 12.00 ogni giorno.

- **Dati fornitori:** provengono da diversi fornitori e sono archiviati
  in un database Snowflake. Vengono aggiornati alle 00.00 ogni giorno.

- **Dati clienti:** provengono da Customer Insights e sono archiviati in
  Dataverse. I dati sono sempre aggiornati.

- **Dati dipendenti:** provengono dal sistema HR e sono archiviati in un
  file di esportazione in una cartella di SharePoint. Vengono aggiornati
  ogni mattina alle 9.00.

    ![](../media/Lab-01/image4.jpeg)

Attualmente è in fase di creazione un modello semantico in Power BI
Premium che estrae i dati dai precedenti sistemi di origine per
soddisfare le esigenze di creazione report e fornire agli utenti finali
la funzionalità self-service. Si usa Power Query per aggiornare il
modello.

**Si devono affrontare le seguenti problematiche:**

- È necessario aggiornare il set di dati almeno tre volte al giorno per
  adattarsi ai diversi tempi di aggiornamento delle diverse origini
  dati.

- Gli aggiornamenti richiedono molto tempo in quanto è necessario
  eseguire un aggiornamento completo ogni volta per acquisire eventuali
  aggiornamenti dei sistemi di origine.

- Se si verificano errori in qualsiasi delle origini dati da cui si
  estraggono i dati, l'aggiornamento del set di dati si interrompe.
  Spesso il file dei dipendenti non viene caricato in tempo e ciò causa
  l'interruzione dell'aggiornamento del set di dati.

- Eventuali modifiche al modello di dati richiedono molto tempo in
  quanto Power Query richiede molto tempo per l'aggiornamento delle
  anteprime, date le dimensioni elevate dei dati e le trasformazioni
  complesse.

- È necessario un PC Windows per usare Power BI Desktop anche se lo
  standard aziendale è Mac.

Hai sentito parlare di Microsoft Fabric e hai deciso di provarlo per
verificare se può risolvere queste problematiche.

### **Panoramica del report di Power BI Desktop**

Prima di iniziare con Fabric, esaminiamo l'attuale report in Power BI
Desktop per comprendere le trasformazioni e il modello.

## Attività 1 - Impostazione di Power BI Desktop nell'ambiente lab

1. Aprire il file **FAIAD.pbix** contenuto nella cartella **Reports**
    sul **Desktop** dell'ambiente lab. Il file si aprirà in Power BI
    Desktop.

    ![](../media/Lab-01/image6.png)

2. Quando si apre la finestra di dialogo "Immettere l'indirizzo di
    posta elettronica", copiare il **Nome utente** e incollarlo nel
    campo **Posta elettronica** della finestra di dialogo, quindi
    selezionare **Continua**.

    - **Posta elettronica/nome utente:** <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-01/image7.png)

3. Immettere i dati Posta elettronica/nome utente seguenti nella
    schermata di accesso visualizzata nella scheda Accedi a Microsoft
    Azure, quindi fare clic su **Avanti**.

    - **Posta elettronica/nome utente:** <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-01/image8.png)

4. Immettere il **Pass di accesso temporaneo** seguente e fare clic su
    **Accedi**.

    - **Pass di accesso temporaneo:** <inject key="AzureAdUserPassword"></inject>

       ![](../media/Lab-01/image9.png)

5. Si apre la finestra di dialogo **Rimani connesso a tutte le tue
    app**. Selezionare **OK**.

    ![](../media/Lab-01/image10.png)

6. **È tutto pronto.** Si apre la finestra di dialogo. Seleziona
    **Fatto**.

Si aprirà Power BI Desktop.

## Attività 2 - Analisi del report di Power BI Desktop

Il report seguente analizza le vendite per Fabrikam. I KPI sono elencati
in alto a sinistra nella pagina. Gli oggetti visivi rimanenti
evidenziano le vendite nel tempo, per area, gruppo di prodotti e azienda
rivenditrice.

  ![](../media/Lab-01/image11.jpeg)

  >**Nota:** in questo corso di formazione ci concentreremo
  sull'acquisizione, la trasformazione e la modellazione dei dati
  mediante gli strumenti disponibili in Fabric. Non ci concentreremo sullo
  sviluppo di report né sullo spostamento al loro interno. Dedichiamo
  qualche minuto alla comprensione del report prima di procedere ai
  passaggi successivi.

1. Analizziamo i dati per area di vendita. Selezionare **New England
    nel grafico a dispersione Sales Territory**. In Sales over time
    notare che il rivenditore Tailspin Toys presenta più vendite di
    Wingtip Toys in New England. Se si considera l'istogramma % vendite
    rispetto all'anno precedente, si noterà che la crescita delle
    vendite di Wingtip Toys è stata bassa ed è calata di trimestre nello
    scorso anno. Dopo un leggero rialzo nel terzo trimestre è nuovamente
    calata nel quarto.

    ![](../media/Lab-01/image12.jpeg)

2. Confrontiamo questi dati con l'area delle Montagne Rocciose.
    Selezionare **Rocky Mountain nel grafico a dispersione Sales
    Territory**. Dall'istogramma % vendite rispetto all'anno
    precedente risulta che le vendite per Wingtip Toys sono aumentate
    notevolmente nel quarto trimestre del 2023 dopo essere state basse
    nei due trimestri precedenti.

    ![](../media/Lab-01/image13.jpeg)

3. Selezionare **Rocky Mountain in Sales Territory** per rimuovere il
    filtro.

4. Nel grafico a dispersione in basso al centro della schermata (ordini
    cliente rispetto alle vendite) selezionare l'outlier in alto a
    destra (4° quadrante). La percentuale di margine è pari al 52%,
    superiore alla media del 50%. Inoltre, la percentuale di vendite
    rispetto all'anno precedente è aumentata negli ultimi due trimestri
    del 2023.

    ![](../media/Lab-01/image14.jpeg)

5. Selezionare il Reseller outlier nel grafico a dispersione per
    **rimuovere il filtro**.

6. Otteniamo i dettagli del prodotto per gruppo di prodotti e
    rivenditore. Nel grafico a barre Vendite per gruppo di prodotti e
    azienda rivenditrice **fare clic con il pulsante destro del
    mouse sulla barra Packaging Materials per Tailspin Toys** e nella
    finestra di dialogo selezionare **Drill-through -> Product
    Detail**.

    ![](../media/Lab-01/image15.png)

7. Si passerà alla pagina che fornisce i dettagli del prodotto. Notare
    che sono anche presenti alcuni ordini futuri.

8. Dopo aver esaminato questa pagina, selezionare **CTRL + freccia
    indietro** in alto a sinistra nella pagina per tornare al report
    vendite.

    ![](../media/Lab-01/image16.png)

9. Se lo si desidera, analizzare ulteriormente il report, dopodiché
    esamineremo la vista modello. Nel pannello a sinistra selezionare
    **l'icona della vista modello**.

    ![](../media/Lab-01/image17.png)

10. Ci sono due tabelle dei fatti Sales e PO.

    a. La granularità dei dati di Sales è per Date, Reseller, Product e
    People. Date, Reseller, Product e People si collegano a Sales.

    b. La granularità dei dati di PO è per Date, Product e People.
    Date, Product e People si collegano a PO.

    c. Sono presenti dati di Supplier per Product. Supplier si collega
    a Product.

    d. Sono presenti dati località di Reseller per Geo. Geo si collega
    a Reseller.

    e. Sono presenti informazioni di Customer per Reseller. Customer si
    collega a Reseller.

## Attività 3 - Analisi delle query in Power Query

1. Osserviamo Power Query per comprendere le origini dati. Nella barra
    multifunzione selezionare **Home -> Trasforma dati**.

    ![](../media/Lab-01/image18.png)

2. Si apre la finestra Power Query. Nella barra multifunzione
    selezionare **Home -> Impostazioni origine dati**. Si apre la
    finestra di dialogo Impostazioni origine dati. Scorrendo l'elenco
    si noterà che vi sono quattro origini dati, come indicato
    nell'esposizione del problema:

    - Snowflake

    - SharePoint

    - ADLS Gen2

    - Dataverse

3. Selezionare **Chiudi** per chiudere la finestra di dialogo
    Impostazioni origine dati.

    ![](../media/Lab-01/image19.png)

4. Nel pannello Query a sinistra, le query sono raggruppate per origine
    dati.

5. Notare che la cartella **DataverseData** contiene dati di Customer
    disponibili in quattro query diverse, ovvero BabyBoomer, GenX, GenY
    e GenZ. Queste quattro query vengono accodate per creare la query
    Customer.

6. Fare clic sulla query **Customer** nella finestra Query. Se si
    seleziona questa query, è necessario reinserire le proprie
    credenziali Dataverse. Fare clic su **Modifica credenziali**.

    ![](../media/Lab-01/image20.png)

7. Fare clic su **Accedi** per accedere al proprio account.

    ![](../media/Lab-01/image21.png)

8. È possibile immettere le credenziali per l'origine dati Dataverse
    immettendo **Nome utente** e **Password**. Le credenziali vengono
    fornite di seguito. Al termine, selezionare **Connetti**.

    - **E-mail/Nome utente:** <inject key="AzureAdUserEmail"></inject>

    - **Password:** <inject key="AzureAdUserPassword"></inject>

9. Fare clic sulla query **ADLS Base Folder** nella finestra Query.
    Alla selezione di questa query verranno richieste le credenziali.
    Fare clic su **Modifica credenziali**.

    ![](../media/Lab-01/image22.png)

10. Per l'origine dati ADLS, scegliere l'opzione **Firma di accesso**
    **condiviso (SAS)** e immettere il **token SAS** fornito in
    precedenza. Selezionare **Connetti**.

    - **Token SAS:** <inject key="Sas token"></inject>

      ![](../media/Lab-01/image23.png)

11. La cartella **ADLSData** include più dimensioni: Geo, Product,
    Reseller e Date. Include anche i fatti Sales.

    - Si crea la **dimensione Geo** unendo i dati dalle query Cities,
      Countries e States.

    - Si crea la **dimensione Product** unendo i dati dalle query
      Product Groups e Product Item Group.

    - Si filtra la **dimensione Reseller** usando la query BuyingGroup.

    - Si crea il **fatto Sales** unendo le query InvoiceLineItems e
      Invoice.

12. Per l'origine dati Snowflake, selezionare la query
    **SupplierCategories** nella finestra Query. Alla selezione di
    questa query verranno richieste le credenziali. Fare clic su
    **Modifica credenziali**.

    ![](../media/Lab-01/image24.png)

13. Immettere il **Nome utente Snowflake** e la **Password Snowflake**
    forniti di seguito. Usare queste credenziali per connettere tutte le
    tabelle in Snowflake a Snowflake, quindi selezionare **Connetti**.

    - **Nome utente Snowflake:** <inject key="SnowFlake Username" enableCopy="false" />

    - **Password Snowflake:** <inject key="SnowFlake Password" enableCopy="false" />

    >**Nota:** se si verificano problemi di connessione a Snowflake con le
    credenziali descritte sopra, usare le credenziali di backup fornite di
    seguito.*

    - **Nome utente Snowflake:** SNOWFLAKE_BACKUP

    - **Password Snowflake:** 8UpfRpExVDXv2AC1

14. Notare che la cartella SnowflakeData include la dimensione Supplier
    e il fatto PO (ordine/spesa).

    - Si crea **dimensione Supplier** unendo le query Suppliers e
      SupplierCategories.

    - Si crea il **fatto PO** unendo le query PO e PO Line Items.

15. Per l'origine dati SharePoint, selezionare la query **People**
    nella finestra Query. Alla selezione di questa query verranno
    richieste le credenziali. Fare clic su **Modifica credenziali**.

    ![](../media/Lab-01/image25.png)

16. Selezionare l'opzione **Account Microsoft**, quindi fare clic su
    **Accedi**. Immettere il nome utente e la password forniti di
    seguito, quindi selezionare Connetti.

    - **E-mail/Nome utente:** <inject key="AzureAdUserEmail"></inject>

    - **Password:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-01/image26.png)

17. La cartella **SharepointData** include la dimensione People.

    ![](../media/Lab-01/image27.png)

    Ora conosciamo gli elementi con cui dobbiamo lavorare. Nel lab seguenti
    creeremo una query di Power Query analoga usando Dataflow Gen2 e un
    modello mediante un lakehouse.

# Riferimenti

Fabric Analyst in a Day (FAIAD) presenta alcune delle funzionalità
chiave disponibili in Microsoft Fabric. Nel menu di servizio, la sezione
Guida (?) include collegamenti ad alcune risorse utili.

  ![](../media/Lab-01/image28.png)

Di seguito sono indicate altre risorse utili a progredire nell'uso di
Microsoft Fabric.

- Vedere il post di blog per leggere [l'annuncio completo sulla
  disponibilità generale di Microsoft
  Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Esplorare Fabric attraverso la [Presentazione
  guidata](https://aka.ms/Fabric-GuidedTour)

- Iscriversi alla versione di [valutazione gratuita di Microsoft
  Fabric](https://aka.ms/try-fabric)

- Visitare il [sito Web di Microsoft
  Fabric](https://aka.ms/microsoft-fabric)

- Acquisire nuove competenze esplorando i [moduli di apprendimento su
  Fabric](https://aka.ms/learn-fabric)

- Consultare la [documentazione tecnica di
  Fabric](https://aka.ms/fabric-docs)

- Leggere [l'e-book gratuito introduttivo a
  Fabric](https://aka.ms/fabric-get-started-ebook)

- Unirsi alla [community di Fabric](https://aka.ms/fabric-community) per
  pubblicare domande, condividere feedback e imparare dagli altri

Leggere i blog di annunci più approfonditi sull'esperienza Fabric:

- [Blog sull'esperienza Data Factory in
  Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Blog sull'esperienza Synapse Data Engineering in
  Fabric](https://aka.ms/Fabric-DE-Blog)

- [Blog sull'esperienza Synapse Data Science in
  Fabric](https://aka.ms/Fabric-DS-Blog)

- [Blog sull'esperienza Synapse Data Warehousing in
  Fabric](https://aka.ms/Fabric-DW-Blog)

- [Blog sull'esperienza Synapse Real-Time Analytics in
  Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog di annunci di Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Blog sull'esperienza Data Activator in
  Fabric](https://aka.ms/Fabric-DA-Blog)

- [Blog su amministrazione e governance in
  Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Blog su OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog sull'integrazione di Dataverse e Microsoft
  Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2025 Microsoft Corporation. Tutti i diritti sono riservati.

L'uso della demo/del lab implica l'accettazione delle seguenti
condizioni:

La tecnologia/le funzionalità descritte nella demo/nel lab sono fornite
da Microsoft Corporation allo scopo di ottenere feedback dall'utente e
offrire un'esperienza di apprendimento. L'utilizzo della demo/del lab
è consentito solo per la valutazione delle caratteristiche e delle
funzionalità di tale tecnologia e per l'invio di feedback a Microsoft.
L'utilizzo per qualsiasi altro scopo non è consentito. È vietato
modificare, copiare, distribuire, trasmettere, visualizzare, eseguire,
riprodurre, pubblicare, concedere in licenza, usare per la creazione di
lavori derivati, trasferire o vendere questa demo/questo lab o parte di
essi.

SONO ESPLICITAMENTE PROIBITE LA COPIA E LA RIPRODUZIONE DELLA DEMO/DEL
LAB (O DI QUALSIASI PARTE DI ESSI) IN QUALSIASI ALTRO SERVER O IN
QUALSIASI ALTRA POSIZIONE PER ULTERIORE RIPRODUZIONE O RIDISTRIBUZIONE.

QUESTA DEMO/QUESTO LAB RENDONO DISPONIBILI TECNOLOGIE
SOFTWARE/FUNZIONALITÀ DI PRODOTTO SPECIFICHE, INCLUSI NUOVI CONCETTI E
NUOVE FUNZIONALITÀ POTENZIALI, IN UN AMBIENTE SIMULATO, CON
UN'INSTALLAZIONE E UNA CONFIGURAZIONE PRIVE DI COMPLESSITÀ, PER GLI
SCOPI DESCRITTI IN PRECEDENZA. LA TECNOLOGIA/I CONCETTI RAPPRESENTATI IN
QUESTA DEMO/IN QUESTO LAB POTREBBERO NON CONTENERE LE FUNZIONALITÀ
COMPLETE E IL LORO FUNZIONAMENTO POTREBBE NON ESSERE LO STESSO DELLA
VERSIONE FINALE. È ANCHE POSSIBILE CHE UNA VERSIONE FINALE DI TALI
FUNZIONALITÀ O CONCETTI NON VENGA RILASCIATA. L'ESPERIENZA D'USO DI
TALI CARATTERISTICHE E FUNZIONALITÀ PUÒ RISULTARE DIVERSA IN UN AMBIENTE
FISICO.

**FEEDBACK.** L'invio a Microsoft di feedback sulle caratteristiche,
sulle funzionalità e/o sui concetti della tecnologia descritti in questa
demo/questo lab implica la concessione a Microsoft, a titolo gratuito,
del diritto di utilizzare, condividere e commercializzare tale feedback
in qualsiasi modo e per qualsiasi scopo. Implica anche la concessione a
titolo gratuito a terze parti del diritto di utilizzo di eventuali
brevetti necessari per i loro prodotti, le loro tecnologie e i loro
servizi al fine di utilizzare o interfacciarsi ai componenti software o
ai servizi Microsoft specifici che includono il feedback. L'utente si
impegna a non inviare feedback la cui inclusione all'interno di
software o documentazione Microsoft imponga a Microsoft di concedere in
licenza a terze parti tale software o documentazione. Questi diritti
sussisteranno anche dopo la scadenza del presente contratto.

CON LA PRESENTE MICROSOFT CORPORATION NON RICONOSCE ALCUNA GARANZIA O
CONDIZIONE RELATIVAMENTE ALLA DEMO/AL LAB, INCLUSE TUTTE LE GARANZIE E
CONDIZIONI DI COMMERCIABILITÀ, DI FATTO ESPRESSE, IMPLICITE O PRESCRITTE
DALLA LEGGE, ADEGUATEZZA PER UNO SCOPO SPECIFICO, TITOLARITÀ E NON
VIOLABILITÀ. MICROSOFT NON OFFRE GARANZIE O RAPPRESENTAZIONI IN
RELAZIONE ALL'ACCURATEZZA DEI RISULTATI E DELL'OUTPUT DERIVANTI
DALL'USO DELLA DEMO/DEL LAB O ALL'ADEGUATEZZA DELLE INFORMAZIONI
CONTENUTE NELLA DEMO/NEL LAB PER QUALSIASI SCOPO.

**CLAUSOLA DI RESPONSABILITÀ**

Questa demo/questo lab contiene solo una parte delle nuove funzionalità
e dei miglioramenti in Microsoft Power BI. Alcune funzionalità
potrebbero cambiare nelle versioni future del prodotto. In questa
demo/in questo lab si apprendono alcune delle nuove funzionalità, ma non
tutte.

