---
title: Parametri obbligatori e facoltativi
TOCTitle: Parametri obbligatori e facoltativi
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56269991
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Parametri obbligatori e facoltativi

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I parametri di Windows PowerShell appartengono a due categorie, ovvero quella dei parametri obbligatori e quella dei parametri facoltativi. Un *parametro obbligatorio* è un parametro che deve essere incluso quando si esegue il comando. Ad esempio, il cmdlet [Remove-CsUserAcp](remove-csuseracp.md) viene usato per annullare l'assegnazione di un provider di servizi di audioconferenza in precedenza assegnato a un utente. Quando si esegue il cmdlet **the Remove-CsUserAcp**, è necessario includere il parametro Identity. Questo parametro comunica al cmdlet per quale utente deve essere rimosso il provider dei servizi di audioconferenza. Come è facile intuire, l'esecuzione di questo comando senza alcun parametro non avrebbe molto senso:

    Remove-CsUserAcp

In questo caso infatti per il cmdlet non sarebbe chiaro per quale utente rimuovere il provider dei servizi di audioconferenza. Per questo motivo, è necessario specificare il parametro Identity dell'utente:

    Remove-CsUserAcp -Identity "Ken Myer"

In Windows PowerShell viene in genere visualizzato un avviso quando si omette un parametro obbligatorio e si tenta di eseguire un comando. Si supponga ad esempio di digitare il comando seguente e premere INVIO:

    Remove-CsUserAcp

Windows PowerShell non eseguirà questo comando incompleto, ma avviserà della mancanza di un parametro obbligatorio:

    Cmdlet Remove-CsUserAcp nella posizione 1 della pipeline dei comandi
    Specificare i valori per i seguenti parametri:
    Identity:

Se si immette un parametro Identity valido e si preme INVIO, Windows PowerShell eseguirà il cmdlet **Remove-CsUserAcp** rimuovendo il provider dei servizi di audioconferenza. Se si decide di non eseguire il comando, è sufficiente premere CTRL+C per terminare il comando.

Poiché questo non è un sistema infallibile, Windows PowerShell non è sempre in grado di richiedere il set di parametri necessario. Alcuni cmdlet sono ad esempio costruiti in modo da rendere obbligatorio l'uso del parametro A o del parametro B, ma non di entrambi. Windows PowerShell potrebbe richiedere di specificare entrambi i parametri A e B e in questo caso il comando non verrebbe eseguito correttamente perché non è possibile usare il parametro A e il parametro B nello stesso comando. Per evitare che si verifichino casi come questo, è consigliabile includere tutti i parametri obbligatori prima di eseguire il comando senza attendere che Windows PowerShell richieda di specificare le informazioni necessarie.

Si noti inoltre che la formattazione del valore del parametro può a volte risultare un processo non proprio intuitivo. Quando ad esempio si include il valore di un parametro che contiene uno spazio vuoto, è necessario racchiudere tale valore tra virgolette doppie:

    -Identity "Ken Myer"

L'utilizzo delle virgolette è tuttavia necessario solo quando si digita il parametro e il valore del parametro come parte del comando da eseguire. Se si tenta di eseguire il cmdlet **Remove-CsUserAcp** dimenticando inavvertitamente di specificare il parametro Identity, Windows PowerShell richiederà di inserire il parametro Identity per l'utente:

    Cmdlet Remove-CsUserAcp nella posizione 1 della pipeline dei comandi Specificare i valori per i seguenti parametri: Identity:

Sarà quindi necessario digitare Ken Myer con il parametro Identity racchiuso tra virgolette doppie:

    Cmdlet Remove-CsUserAcp nella posizione 1 della pipeline dei comandi Specificare i valori per i seguenti parametri: "Ken Myer"

Se si procede in questo modo, il comando non verrà eseguito correttamente:

    Remove-CsUserAcp : Oggetto di gestione non trovato per l'identità ""Ken Myer"".

In questo caso è stata eseguita la ricerca di un utente con identità "Ken Myer", con le virgolette doppie incluse come parte del parametro Identity. Se viene richiesto di immettere un valore per il parametro, non includere le virgolette doppie:

    cmdlet Remove-CsUserAcp nella posizione 1 della pipeline dei comandi Specificare i valori per i seguenti parametri:
    Identity: Ken Myer

Un *parametro facoltativo* è invece esattamente ciò che il nome indica, ovvero un parametro che non deve necessariamente essere immesso affinché il comando venga eseguito. Ad esempio, per Remove-CsUserAcp esiste il parametro facoltativo Name. Se si include il parametro Name nel comando, viene rimosso solo il provider dei servizi di audioconferenza specificato. Questo comando rimuove il provider dei servizi di audioconferenza denominato Fabrikam ACP ma non rimuove alcun altro provider assegnato a Ken Myer:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

Se non si specifica questo parametro facoltativo, il comando viene eseguito ugualmente. In questo caso Remove-CsUserAcp eliminerà tuttavia tutti i provider dei servizi di audioconferenza assegnati a Ken Myer:

    Remove-CsUserAcp -Identity "Ken Myer"

## Vedere anche

#### Concetti

[Introduzione a Windows PowerShell e Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

