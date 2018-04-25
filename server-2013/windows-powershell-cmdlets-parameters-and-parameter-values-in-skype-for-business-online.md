---
title: Cmdlet, parametri e valori di parametro di Windows PowerShell
TOCTitle: Cmdlet, parametri e valori di parametro di Windows PowerShell
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56269878
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet, parametri e valori di parametro di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Se si conosce già la finestra di comando disponibile in tutte le versioni di Windows o se si ha familiarità con MS-DOS, sarà più facile apprendere come usare Windows PowerShell. Nella finestra di comando si digita un comando e si preme INVIO. In risposta, il computer esegue un comando o un file eseguibile. Per visualizzare ad esempio informazioni su tutti i file e tutte le cartelle nella directory corrente, digitare il comando seguente al prompt dei comandi e quindi premere INVIO:

    dir

Verranno visualizzate informazioni su tutti i file e tutte le cartelle disponibili nella directory corrente:

``` 
    Directory: C:\

21/03/2013  15.39    <DIR>          Deploy
21/03/2013  14.55    <DIR>          Intel
26/07/2012  12.33    <DIR>          PerfLogs
10/04/2013  10.29    <DIR>          Program Files
08/04/2013  10.28    <DIR>          Program Files (x86)
22/03/2013  08.44    <DIR>          Users
11/04/2013  15.00    <DIR>              Windows
13/03/2013  14.53                 117   pldok.log
21/03/2013  15.35                 769   RHDSetup.exe
21/03/2013  15.37            207   setup.doc
              3 File        1.093 byte
              7 Directory 21.386.002.432 byte disponibili
```

Questo è un esempio del risultato che si ottiene digitando solo il nome di un comando o di un file eseguibile, tuttavia, molti dei comandi eseguiti dalla finestra di comando accettano anche *argomenti*. Gli argomenti sono informazioni aggiuntive passate al comando che ne modificano il comportamento. Ad esempio, se si desidera vedere solo i nomi dei file e delle cartelle nella directory corrente, senza altre informazioni come le dimensioni del file o della cartella oppure la data e l'ora di creazione, si aggiungerà l'argomento **/b** al comando dir:

    dir /b

Quando si include l'argomento **/b**, il comando **dir** restituisce solo i nomi delle cartelle e dei file trovati nella directory corrente:

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

Nel comando precedente l'argomento **/b** è la sola informazione richiesta per limitare i dati restituiti a nomi di file e cartelle. Questo è spesso il modo in cui vengono usati i comandi della riga di comando: basta la presenza di un argomento per modificarne il comportamento. In pratica, si include l'argomento **/b** per nascondere informazioni aggiuntive o si esclude l'argomento **/b** per mostrare altre informazioni. A volte è tuttavia necessario specificare un *valore dell'argomento*, ovvero informazioni aggiuntive passate all'argomento stesso. Ad esempio, l'argomento **/o** consente di specificare come dovranno essere ordinati i dati restituiti dal comando dir. Tra le altre opzioni è possibile usare il valore dell'argomento **e** per ordinare i risultati in base all'estensione di file o il valore dell'argomento **s** per ordinarli in base alle dimensioni dei file. Il comando seguente ordina ad esempio i dati restituiti in base all'estensione di file. Si noti come il valore dell'argomento **e** sia incluso immediatamente dopo l'argomento **/o**:

    dir /oe

Per la cartella di esempio i dati restituiti avranno il seguente aspetto, con i file elencati in ordine alfabetico per estensione:

``` 
    Directory: C:\

21/03/2013  15.39    <DIR>          Deploy
21/03/2013  14.55    <DIR>          Intel
26/07/2012  12.33    <DIR>          PerfLogs
10/04/2013  10.29    <DIR>          Program Files
08/04/2013  10.28    <DIR>          Program Files (x86)
22/03/2013  08.44    <DIR>          Users
11/04/2013  15.00    <DIR>              Windows
21/03/2013  15.37            207   setup.doc
21/03/2013  15.35                 769   RHDSetup.exe
13/03/2013  14.53                 117   pldok.log
              3 File        1.093 byte
              7 Directory 21.386.002.432 byte disponibili
```

Ovvero, per maggiore chiarezza:

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

Anche se in Windows PowerShell viene usata una terminologia diversa, l'approccio di base per l'uso di Windows PowerShell è lo stesso adottato nella finestra di comando: si digitano i comandi, si includono argomenti e valori dell'argomento, se necessario, e quindi si preme INVIO per eseguire i comandi. Come detto, in Windows PowerShell viene tuttavia usata una terminologia diversa rispetto alla shell dei comandi. In Windows PowerShell i comandi eseguiti sono detti *cmdlets*, mentre gli argomenti passati a un cmdlet sono noti come *parametri* e i valori passati ai parametri come *valori del parametro*.

Le definizioni precedenti sono alquanto semplificate. I cmdlets sono essenzialmente mini-applicazioni che possono essere eseguite solo dall'ambiente Windows PowerShell. È tuttavia possibile eseguire altri comandi e applicazioni da Windows PowerShell, inclusa la maggior parte dei comandi e delle applicazioni eseguibili da una finestra di comando. Per avviare ad esempio il Blocco note da Windows PowerShell, basta digitare quanto segue e premere INVIO:

    notepad.exe

Per la gestione di Skype for Business online, la maggior parte degli amministratori ricorre tuttavia ai cmdlet di Windows PowerShell per eseguire attività amministrative. A volte sono disponibili pochi altri tipi di comandi o applicazioni utilizzabili per gestire Skype for Business online. Qualche volta i cmdlet di Skype for Business online possono essere usati senza argomenti aggiuntivi (come detto, gli argomenti sono noti come parametri in Windows PowerShell). Il seguente comando chiama ad esempio il cmdlet [Get-CsOnlineUser](get-csonlineuser.md) senza parametri aggiuntivi. Il comando da solo restituisce informazioni su tutti gli utenti di Skype for Business online:

    Get-CsOnlineUser

La maggior parte dei cmdlet di Skype for Business online accetta tuttavia parametri e valori di parametro. Si consideri il comando seguente:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Questo comando è composto da tre parti:

  - Il cmdlet **Get-CsOnlineUser**.

  - Il parametro Identity. Si noti che in Windows PowerShell i parametri sono sempre preceduti da un trattino (-). Ciò significa che per questo stesso cmdlet il parametro UnassignedUser verrebbe indicato usando la sintassi seguente:
    
        -UnassignedUser
    
    Questa informazione è utile non solo perché i parametri devono essere preceduti da un trattino, ma anche perché l'uso è diverso rispetto alla finestra di comando dove gli argomenti sono preceduti da una barra (/):
    
    ``` 
    /b
    ```

  - Il valore del parametro **kenmyer@litwareinc.com**.

Per inciso, questo comando restituisce informazioni su un utente specifico, quello con l'identità kenmyer@litwareinc.com.

## Vedere anche

#### Concetti

[Introduzione a Windows PowerShell e Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

