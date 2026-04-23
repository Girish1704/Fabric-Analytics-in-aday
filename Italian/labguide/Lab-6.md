# Microsoft Fabric - Fabric Analyst in a Day - Lab 6

![](../media/Lab-6/H6.png)

# Sommario

- Introduzione

- Lakehouse: analisi di dati

    - Attività 1: Query sui dati mediante SQL

    - Attività 2: Visualizzazione del risultato T-SQL

- Lakehouse: modellazione semantica

    - Attività 3: Creazione di un modello semantico

    - Attività 4: Creazione di relazioni

    - Attività 5: Creazione delle misure

    - Attività 6: Sezione facoltativa: creazione delle relazioni

    - Attività 7: Sezione facoltativa: creazione delle misure

- Riferimenti

# Introduzione

Abbiamo inserito dati provenienti da diverse origini dati in Lakehouse. In questo lab si lavorerà con il modello semantico. In genere, eseguiamo attività di modellazione quali la creazione di relazioni, l'aggiunta di misure, ecc. in Power BI Desktop. Qui impareremo a eseguire queste attività di modellazione nel servizio.

In questo lab si apprenderà quanto segue:

- Uso della vista SQL nell'endpoint di Analisi SQL

- Come creare un modello semantico

# Lakehouse: analisi di dati

## Attività 1: Query sui dati mediante SQL

1. Torniamo all'area di lavoro di Fabric **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** creata nel Lab 2, Attività 8.

2. Se si preferisce, è possibile **ridurre a icona il flusso di attività** per visualizzare l'elenco completo degli elementi.

3. Saranno visibili tre elementi associati a lh_FAIAD, ovvero il lakehouse, il modello semantico e l'endpoint SQL. In un lab precedente abbiamo esaminato il lakehouse e creato query visive usando l'endpoint di Analisi SQL. Seleziona l'icona **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** nel riquadro di spostamento a sinistra e scegli l'opzione **Endpoint di analisi SQL lh_FAIAD** per continuare a esplorare questa opzione. Si aprirà la **vista SQL** di Explorer.

    ![](../media/Lab-6/image6.png)

    Se si desidera esplorare i dati prima di creare un modello di dati, è possibile usare SQL a questo fine. Sono disponibili due opzioni per usare SQL. La prima opzione è la query visiva, che abbiamo usato nel lab precedente. La seconda opzione è la scrittura di codice T-SQL. Si tratta di un'opzione pensata per gli sviluppatori. Esaminiamola assieme.

    Supponiamo di voler conoscere rapidamente le unità Units dal fornitore mediante SQL.

    Nell'endpoint di Analisi SQL del lakehouse, come indicato nel pannello di sinistra, è possibile visualizzare le tabelle. Espandendo le tabelle, si possono visualizzare le colonne che compongono la tabella. Vi sono inoltre opzioni per la creazione di viste SQL, funzioni e stored procedure. Se si ha familiarità con SQL, è possibile esplorare queste opzioni. Proviamo a scrivere una semplice query SQL.

4. Nel **menu in alto** selezionare **Nuova query SQL** oppure, al centro dello schermo, fare clic su **Nuova query SQL.** Si aprirà la vista della query SQL.

    ![](../media/Lab-6/image7.png)

5. Incollare la **query SQL seguente** nella **finestra della query**. Questa query restituirà le unità in base al nome del fornitore. Per ottenere questo risultato è necessario unire la tabella Sales alle tabelle Product e Supplier.

    ```sql
   SELECT su.SupplierName, SUM(Quantity) as Units
   FROM dbo.Sales s
   JOIN dbo.Product p on p.StockItemID = s.StockItemID
   JOIN dbo.Supplier su on su.SupplierID = p.SupplierID
   GROUP BY su.SupplierName
   ```

6. Fare clic su **Esegui** nel menu dell'editor SQL per visualizzare i risultati.

7. Notare che è disponibile un'opzione per salvare questa query come vista selezionando **Salva come visualizzazione**.

8. Nel pannello di **sinistra** **Explorer**, nella sezione **Query** notare che questa query è salvata in **Query personali** come **SQL query 1**. Ciò consente di rinominare la query e salvarla per l'uso futuro. È inoltre presente un'opzione per visualizzare le query condivise con l'utente corrente mediante la cartella **Query condivise**.

    >**Nota:** le query visive create nei lab precedenti sono disponibili anche nella cartella My queries.

    ![](../media/Lab-6/image8.png)

## Attività 2: Visualizzazione del risultato T-SQL

1. Possiamo anche visualizzare il risultato di questa query. **Evidenziare la query** nel riquadro delle query

2. Nel menu del riquadro Risultati, seleziona l'icona del menu a discesa -> **Visualizza risultati**.

    ![](../media/Lab-6/image9.png)

3. Si apre la finestra di dialogo **Visualizza risultati** . Selezionare **Continua**.

    Si apre la finestra di dialogo **Visualizza risultati** che ha un aspetto simile alla vista del report Power BI Desktop. Presenta tutte le funzionalità disponibili nella vista del report Power BI Desktop: è possibile formattare la pagina, selezionare diversi oggetti visivi, formattare gli oggetti visivi, aggiungere filtri, ecc. Non esploreremo queste opzioni in questo corso.

4. Espandere il riquadro **Dati**, quindi espandere **Query SQL 1**.

5. Selezionare i campi **Supplier_Name** e **Units**. Viene creato un oggetto visivo tabella.

    ![](../media/Lab-6/image10.png)

6. Nella sezione **Visualizzazioni** cambiare il tipo di oggetto visivo selezionando l'**istogramma in pila**.

7. Selezionare **Salvare come report** in basso a destra della schermata.

    ![](../media/Lab-6/image11.png)

8. Si apre la finestra di dialogo Salva il report. Digitare **Units per fornitore** nella casella di testo **Immettere un nome per il report**.

9. Assicurarsi che l'area di lavoro di destinazione sia l'area di lavoro di Fabric, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**

10. Selezionare **Salva**.

    ![](../media/Lab-6/image12.png)

    Si aprirà nuovamente la schermata Query SQL.

# Lakehouse: modellazione semantica

## Attività 3: Creazione di un modello semantico

1. Nel menu dell'endpoint di analisi SQL selezionare **Nuovo modello semantico**.

    ![](../media/Lab-6/image13.png)

2. Viene visualizzata la finestra di dialogo **Nuovo modello semantico**. Immettere **sm_FAIAD** come nome del modello semantico Direct Lake.

3. Per impostazione predefinita abbiamo la possibilità di selezionare un sottoinsieme delle tabelle. tenere presente che nel lab precedente avevamo creato delle viste. Ora vogliamo includere queste viste nel modello. Espandere lo schema **dbo** in cui è possibile vedere tutte le tabelle e le viste del lakehouse.

    ![](../media/Lab-6/image14.png)

4. **Selezionare** le seguenti tabelle/viste:

    1. **Customer**

    2. **Date**

    3. **People**

    4. **PO**

    5. **Supplier**

    6. **Geo**

    7. **Product**

    8. **Reseller**

    9. **Sales**

5. Selezionare **Conferma.**

    ![](../media/Lab-6/image15.png)

    Potrai accedere al nuovo modello semantico con le tabelle selezionate. È possibile **ridisporre** liberamente le tabelle in base alle esigenze. Notare che alcune tabelle (Geo, Reseller, Sales e Product) presentano un segnale di avviso in alto a destra. Questo perché si tratta di viste. Tutti gli oggetti visivi creati con campi a partire da queste viste saranno in modalità Direct Query e non in modalità Direct Lake.

    >**Nota:** la modalità Direct Lake è più veloce della modalità Direct Query.

## Attività 4: Creazione di relazioni

Se non ti trovi attualmente all’interno del nuovo modello semantico creato, andiamo nel punto corretto

1. Torniamo all'area di **lavoro di Fabric** e selezionare il modello semantico **sm_FAIAD**.

    ![](../media/Lab-6/image16.png)

2. Fare clic su **Apri modello semantico.**

    ![](../media/Lab-6/image17.png)

3. Nell'angolo in alto a destra verificare di essere nella modalità **Modifica**.

    ![](../media/Lab-6/image18.png)

4. Il primo passaggio permette di creare relazioni tra queste tabelle.

    ![](../media/Lab-6/image19.png)

5. Creiamo una relazione tra le tabelle Sales e Reseller. Selezionare **ResellerID** dalla tabella **Sales** e trascinarlo su **ResellerID** nella tabella **Reseller**.

    ![](../media/Lab-6/image20.png)

6. Si apre la finestra di dialogo Nuova relazione. Assicurarsi che **Da tabella** sia **Sales** e che la **Colonna** sia **ResellerID.**

7. Assicurarsi che **Nella tabella** sia **Reseller** e che la **Colonna** sia **ResellerID.**

8. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

9. Assicurarsi che il campo **Direzione filtro incrociato** sia impostato su **Singola**.

10. Selezionare **Salva**.

    ![](../media/Lab-6/image21.png)

11. Allo stesso modo, creiamo una relazione tra le tabelle Sales e Date. Selezionare **InvoiceDate** dalla tabella **Sales** e trascinarlo su **Date** nella tabella **Date**.

12. Si apre la finestra di dialogo Nuova relazione. Assicurarsi che **Da tabella** sia **Sales** e che la **Colonna** sia **InvoiceDate.**

13. Assicurarsi che **Nella tabella** sia **Date** e che la **Colonna** sia **Date.**

14. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

15. Assicurarsi che il campo **Direzione filtro incrociato** sia impostato su **Singola**.

16. Selezionare **Salva**.

    ![](../media/Lab-6/image22.png)

17. Analogamente, creare una relazione **molti-a-uno** tra le tabelle **Sales** e **Product**. Selezionare **StockItemID** dalla tabella **Sales** e **StockItemID** dalla tabella **Product**.

    >**Nota:** tutti i nostri aggiornamenti vengono salvati automaticamente.

    >**Checkpoint:** il modello dovrebbe avere le tre relazioni tra le tabelle Sales e Reseller e le tabelle Sales e Date e Sales e Product come mostrato nello screenshot seguente:

    ![](../media/Lab-6/image23.png)

    Per motivi di tempo, non creeremo tutte le relazioni. Se il tempo lo consente, è possibile completare la sezione facoltativa alla fine del laboratorio. La sezione facoltativa illustra i passaggi per creare le relazioni rimanenti.

## Attività 5: Creazione delle misure

Aggiungiamo alcune misure necessarie per creare il dashboard Sales.

1. Selezionare la **tabella Sales** dalla vista del modello. Vogliamo aggiungere le misure alla tabella Sales.

2. Nel menu in alto selezionare **Home -> Nuova misura**. Notare che viene visualizzata
    la barra della formula.

3. Immettere **Sales = SUM(‘Sales’[Sales Amount])** nella **barra della formula**.

4. Fare clic sul **segno di spunta** a sinistra della barra della formula o premere il tasto **INVIO**.

5. Espandere il pannello delle proprietà a destra.

6. Espandere la sezione **Formattazione**.

7. Nel menu a discesa **Formato** selezionare **Valuta**.

8. Impostare Posizioni decimali su **0**.

    ![](../media/Lab-6/image24.png)

9. Con la **tabella** **Sales** selezionata nel menu in alto, selezionare **Home -> Nuova misura**. Notare che viene visualizzata la barra della formula.

10. Immettere **Units = SUM (‘Sales’[Quantity])** nella **barra della formula**.

11. Fare clic sul **segno di spunta** a sinistra della barra della formula o premere il tasto **INVIO**.

12. Nel pannello Proprietà a destra espandere la sezione **Formattazione** (il caricamento del pannello Proprietà potrebbe richiedere alcuni istanti).

13. Nell'elenco a discesa **Formato** selezionare **Numero intero**.

14. Usare il dispositivo di scorrimento per impostare il **Separatore delle migliaia** su **Sì.**

    ![](../media/Lab-6/image25.png)

15. Con la tabella **Sales** selezionata nel menu in alto, selezionare **Home -> Nuova misura**. Notare che viene visualizzata la barra della formula.

16. Immettere **Sales Orders = DISTINCTCOUNT(‘Sales’[InvoiceID])** nella **barra della formula**.

17. Fare clic sul **segno di spunta** a sinistra della barra della formula o premere il tasto **INVIO**.

18. Nel pannello Proprietà a destra espandere la sezione **Formattazione**.

19. Nell'elenco a discesa **Formato** selezionare **Numero intero**.

20. Usare il dispositivo di scorrimento per impostare il **Separatore delle migliaia** su **Sì**.

    ![](../media/Lab-6/image26.png)

21. Nel **pannello dati** (a destra) selezionare **Modello**. Notare che questa operazione fornisce una vista che semplificherà l'organizzazione di tutti gli elementi nel modello semantico.

22. Espandere **Modello semantico -> Misure** per visualizzare tutte le misure appena create.

23. È anche possibile **espandere le singole tabelle** per visualizzare le colonne, le gerarchie e le misure in ciascuna di esse.

    ![](../media/Lab-6/image27.png)

    Anche in questo caso, per motivi di tempo non creeremo tutte le misure. Se il tempo lo consente, è possibile completare la sezione facoltativa alla fine del laboratorio. La sezione facoltativa illustra i passaggi per creare le misure rimanenti.

    Abbiamo creato un modello semantico, il passaggio successivo è creare un report. Ce ne occuperemo nel prossimo lab.

## Attività 6: Sezione facoltativa: creazione delle relazioni

Aggiungiamo le relazioni rimanenti.

1. Nel menu in alto selezionare **Home -> Gestisci relazioni**.

2. Si apre la finestra di dialogo Gestisci relazioni. Selezionare **+ Nuova relazione**.

    ![](../media/Lab-6/image28.png)

3. Si apre la finestra di dialogo Nuova relazione. Assicurarsi che **Da tabella** sia **Sales** e che la **Colonna** sia **SalespersonPersonID.**

4. Assicurarsi che **Nella tabella** sia **People** e che la **Colonna** sia **PersonID.**

5. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

6. Assicurarsi che la **direzione filtro incrociato** sia **Singola**.

7. Selezionare **Salva**. Viene visualizzata la finestra di dialogo Gestisci relazioni con la nuova relazione aggiunta.

    ![](../media/Lab-6/image29.png)

8. Ora creeremo una relazione tra Product e Supplier. Selezionare **+ Nuova relazione**.

9. Assicurarsi che **Da tabella** sia **Product** e che la **Colonna** sia **SupplierID.**

10. Assicurarsi che **Nella tabella** sia **Supplier** e che la **Colonna** sia **SupplierID.**

11. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

12. Assicurarsi che la **direzione filtro incrociato** sia **Entrambe**.

13. Selezionare **Salva**.

    ![](../media/Lab-6/image30.png)

14. Ora creeremo una relazione tra Reseller e Geo. Selezionare **+ Nuova relazione.**

15. Si apre la finestra di dialogo Nuova relazione. Assicurarsi che **Da tabella** sia **Reseller** e che la **Colonna** sia **PostalCityID.**

16. Assicurarsi che **Nella tabella** sia **Geo** e che la **Colonna** sia **CityID.**

17. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

18. Assicurarsi che la **direzione filtro incrociato** sia **Entrambe**.

19. Selezionare **Salva**.

    ![](../media/Lab-6/image31.png)

20. Ora creeremo una relazione tra Customer e Reseller. Selezionare **+ Nuova relazione**.

21. Si apre la finestra di dialogo Nuova relazione. Assicurarsi che **Da tabella** sia **Customer** e che la **Colonna** sia **ResellerID.**

22. Assicurarsi che **Nella tabella** sia **Reseller** e che la **Colonna** sia **ResellerID.**

23. Assicurarsi che il campo **Cardinalità** sia impostato su **Molti a uno (*:1)**.

24. Assicurarsi che la **direzione filtro incrociato** sia **Singola**.

25. Selezionare **Salva**.

    >**Checkpoint:** le relazioni del modello dovrebbero presentarsi come illustrato nello screenshot seguente.

    ![](../media/Lab-6/image32.png)

26. Allo stesso modo, creare una relazione **molti-a-uno** tra le tabelle **PO** e **Date**. Selezionare **Order_Date** da **PO** e **Date** da **Date**.

27. Allo stesso modo, creare una relazione **molti-a-uno** tra le tabelle **PO** e **Product**. Selezionare **StockItemID** da **PO** e **StockItemID** da **Product**.

28. Allo stesso modo, creare una relazione **molti-a-uno** tra le tabelle **PO** e **People**. Selezionare **ContactPersonID** da **PO** e **PersonID** da **People**.

29. Selezionare **Chiudi** per chiudere la finestra di dialogo Gestisci relazioni. Abbiamo creato tutte le relazioni.

    >**Checkpoint:** il modello dovrebbe presentarsi come illustrato nello screenshot seguente.

    ![](../media/Lab-6/image33.png)

## Attività 7: Sezione facoltativa: creazione delle misure

Aggiungiamo le misure rimanenti.

1. Selezionare la tabella **Sales** e nel menu in alto selezionare **Home -> Nuova misura**.

2. Immettere **Avg Order** = **DIVIDE([Sales], [Sales Orders])** nella barra della formula.

3. Fare clic sul **segno di spunta** nella barra della formula o premere il tasto INVIO.

4. Espandere il pannello delle proprietà a destra.

5. Espandere la sezione **Formattazione**.

6. Nel menu a discesa **Formato** selezionare **Valuta**.

7. Impostare Posizioni decimali su 0.

    ![](../media/Lab-6/image34.png)

8. Seguire passaggi analoghi per aggiungere le seguenti misure:

    1. Nella tabella **Sales GM = SUM(‘Sales’[LineProfit])** formattata come **Valuta con 0 posizioni decimali**.

    2. Nella tabella **Sales**, **GM% = DIVIDE([GM], [Sales])** formattato come **Percentuale con 0 posizioni decimali.**

    3. Nella tabella **Customer, No of Customers = COUNTROWS(Customer)** formattato come **Numero intero con separatore delle migliaia abilitato.**

# Riferimenti

Fabric Analyst in a Day (FAIAD) presenta alcune delle funzionalità chiave disponibili in Microsoft Fabric. Nel menu di servizio, la sezione Guida (?) include collegamenti ad alcune risorse utili.

![](../media/Lab-6/image35.png)

Di seguito sono riportate ulteriori risorse utili che consentiranno di progredire nell'uso di Microsoft Fabric.

- Vedere il post di blog per leggere l'[annuncio completo sulla disponibilità generale di Microsoft Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Esplorare Fabric attraverso la [Presentazione guidata](https://aka.ms/Fabric-GuidedTour)

- Iscriversi alla [versione di valutazione gratuita di Microsoft Fabric](https://aka.ms/try-fabric)

- Visitare il [sito Web di Microsoft Fabric](https://aka.ms/microsoft-fabric)

- Acquisire nuove competenze esplorando i [moduli di apprendimento su Fabric](https://aka.ms/learn-fabric)

- Consultare la [documentazione tecnica di Fabric](https://aka.ms/fabric-docs)

- Leggere l'[e-book gratuito introduttivo a Fabric](https://aka.ms/fabric-get-started-ebook)

- Unirsi alla [community di Fabric](https://aka.ms/fabric-community) per pubblicare domande, condividere feedback e imparare dagli altri

Leggere i blog di annunci più approfonditi sull'esperienza Fabric:

- [Blog sull'esperienza Data Factory in Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Blog sull'esperienza Synapse Data Engineering in Fabric](https://aka.ms/Fabric-DE-Blog)

- [Blog sull'esperienza Synapse Data Science in Fabric](https://aka.ms/Fabric-DS-Blog)

- [Blog sull'esperienza Synapse Data Warehousing in Fabric](https://aka.ms/Fabric-DW-Blog)

- [Blog sull'esperienza Synapse Real-Time Analytics in Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog di annunci di Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Blog sull'esperienza Data Activator in Fabric](https://aka.ms/Fabric-DA-Blog)

- [Blog su amministrazione e governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Blog su OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog sull'integrazione di Dataverse e Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Tutti i diritti sono riservati.

L'uso della demo/del lab implica l'accettazione delle seguenti condizioni:

La tecnologia/le funzionalità descritte nella demo/nel lab sono fornite da Microsoft Corporation allo scopo di ottenere feedback dall'utente e offrire un'esperienza di apprendimento. L'utilizzo della demo/del lab è consentito solo per la valutazione delle caratteristiche e delle funzionalità di tale tecnologia e per l'invio di feedback a Microsoft. L'utilizzo per qualsiasi altro scopo non è consentito. È vietato modificare, copiare, distribuire, trasmettere, visualizzare, eseguire, riprodurre, pubblicare, concedere in licenza, usare per la creazione di lavori derivati, trasferire o vendere questa demo/questo lab o parte di essi.

SONO ESPLICITAMENTE PROIBITE LA COPIA E LA RIPRODUZIONE DELLA DEMO/DEL LAB (O DI QUALSIASI PARTE DI ESSI) IN QUALSIASI ALTRO SERVER O IN QUALSIASI ALTRA POSIZIONE PER ULTERIORE RIPRODUZIONE O RIDISTRIBUZIONE.

QUESTA DEMO/QUESTO LAB RENDONO DISPONIBILI TECNOLOGIE SOFTWARE/FUNZIONALITÀ DI PRODOTTO SPECIFICHE, INCLUSI NUOVI CONCETTI E NUOVE FUNZIONALITÀ POTENZIALI, IN UN AMBIENTE SIMULATO, CON UN'INSTALLAZIONE E UNA CONFIGURAZIONE PRIVE DI COMPLESSITÀ, PER GLI SCOPI DESCRITTI IN PRECEDENZA. LA TECNOLOGIA/I CONCETTI RAPPRESENTATI IN QUESTA DEMO/IN QUESTO LAB POTREBBERO NON CONTENERE LE FUNZIONALITÀ COMPLETE E IL LORO FUNZIONAMENTO POTREBBE NON ESSERE LO STESSO DELLA VERSIONE FINALE. È ANCHE POSSIBILE CHE UNA VERSIONE FINALE DI TALI FUNZIONALITÀ O CONCETTI NON VENGA RILASCIATA. L'ESPERIENZA D'USO DI TALI CARATTERISTICHE E FUNZIONALITÀ PUÒ RISULTARE DIVERSA IN UN AMBIENTE FISICO.

**FEEDBACK.** L'invio a Microsoft di feedback sulle caratteristiche, sulle funzionalità e/o sui concetti della tecnologia descritti in questa demo/questo lab implica la concessione a Microsoft, a titolo gratuito, del diritto di utilizzare, condividere e commercializzare tale feedback in qualsiasi modo e per qualsiasi scopo. Implica anche la concessione a titolo gratuito a terze parti del diritto di utilizzo di eventuali brevetti necessari per i loro prodotti, le loro tecnologie e i loro servizi al fine di utilizzare o interfacciarsi ai componenti software o ai servizi Microsoft specifici che includono il feedback. L'utente si impegna a non inviare feedback la cui inclusione all'interno di software o documentazione Microsoft imponga a Microsoft di concedere in licenza a terze parti tale software o documentazione. Questi diritti sussisteranno anche dopo la scadenza del presente contratto.

CON LA PRESENTE MICROSOFT CORPORATION NON RICONOSCE ALCUNA GARANZIA O CONDIZIONE RELATIVAMENTE ALLA DEMO/AL LAB, INCLUSE TUTTE LE GARANZIE E CONDIZIONI DI COMMERCIABILITÀ, DI FATTO ESPRESSE, IMPLICITE O PRESCRITTE DALLA LEGGE, ADEGUATEZZA PER UNO SCOPO SPECIFICO, TITOLARITÀ E NON VIOLABILITÀ. MICROSOFT NON OFFRE GARANZIE O RAPPRESENTAZIONI IN RELAZIONE ALL'ACCURATEZZA DEI RISULTATI E DELL'OUTPUT DERIVANTI DALL'USO DELLA DEMO/DEL LAB O ALL'ADEGUATEZZA DELLE INFORMAZIONI CONTENUTE NELLA DEMO/NEL LAB PER QUALSIASI SCOPO.

**CLAUSOLA DI RESPONSABILITÀ**

Questa demo/questo lab contiene solo una parte delle nuove funzionalità e dei miglioramenti in Microsoft Power BI. Alcune funzionalità potrebbero cambiare nelle versioni future del prodotto. In questa demo/in questo lab si apprendono alcune delle nuove funzionalità, ma non tutte.

