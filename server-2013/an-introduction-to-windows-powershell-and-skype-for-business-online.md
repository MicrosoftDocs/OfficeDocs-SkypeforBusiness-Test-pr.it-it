---
title: Introduzione a Windows PowerShell e Lync Online
TOCTitle: Introduzione a Windows PowerShell e Lync Online
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56269906
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Introduzione a Windows PowerShell e Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Windows PowerShell è una shell dei comandi e un linguaggio di scripting che consente di gestire Skype for Business online. Invece di usare l'interfaccia grafica di amministrazione di Skype for Business online, è possibile gestire Skype for Business online utilizzando comandi della riga di comando analoghi al seguente:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Oltre a eseguire semplici comandi come nell'esempio precedente, che restituisce informazioni sull'utente con UPN kenmyer@litwareinc.com, gli utenti più esperti di Windows PowerShell possono anche organizzare questi comandi in script da usare per automatizzare i processi e/o eseguire attività ripetitive.

In generale, tutte le attività che si possono eseguire mediante l'interfaccia di amministrazione di Skype for Business online possono essere eseguite anche mediante Windows PowerShell. Ad esempio, è possibile usare l'interfaccia di amministrazione per gestire le notifiche sul cellulare, o *notifiche Push*, che consentono di inviare notifiche su eventi (ad esempio nuovi messaggi istantanei o nuovi messaggi vocali) a dispositivi mobili come iPhone e Windows Phone. Queste notifiche possono essere ricevute sul dispositivo mobile anche se l'applicazione Lync su tali dispositivi viene eseguita in background.

Per gestire le notifiche Push è possibile usare l'interfaccia di amministrazione di Skype for Business online, che consente di abilitare o disabilitare le notifiche Push selezionando l'opzione appropriata nella scheda **organizzazione**:

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362807.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

Le notifiche Push possono anche essere abilitate o disabilitate mediante una sessione remota di Windows PowerShell e il cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md). Ad esempio, il comando seguente disabilita le notifiche Push per iPhone e Windows Phone:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Come si nota, i parametri EnableApplePushNotificationService e EnableMicrosoftPushNotificationService usati con il cmdlet **Set-CsPushNotificationConfiguration** corrispondono alle opzioni disponibili nell'interfaccia di amministrazione di Skype for Business online:

![Associazione tra opzioni di Lync e cmdlet di PowerShell](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Associazione tra opzioni di Lync e cmdlet di PowerShell")

Riepilogando, è possibile usare l'interfaccia di amministrazione o un cmdlet di Windows PowerShell con i parametri appropriati per gestire le notifiche Push. Entrambi gli approcci funzionano altrettanto bene.


> [!NOTE]
> Per le definizioni di termini specifici di Windows PowerShell, ad esempio <EM>cmdlet</EM>, <EM>parametro</EM>, <EM>valore del parametro</EM> e <EM>argomento</EM>, vedere <A href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Cmdlet, parametri e valori di parametro di Windows PowerShell</A>.



Se l'interfaccia di amministrazione di Skype for Business online e Windows PowerShell forniscono le stesse identiche funzionalità, nasce spontaneo chiedersi perché scegliere uno piuttosto che l'altro. Anzi, ci si chiederà perché mai si dovrebbe decidere di digitare comandi in Windows PowerShell anziché selezionare o deselezionare semplicemente le caselle di controllo nell'interfaccia di amministrazione.

In un caso semplice come quello precedente, l'approccio scelto è una questione di gusto personale: alcuni preferiscono usare un'interfaccia grafica, mentre altri preferiscono uno strumento da riga di comando, come Windows PowerShell. In alcuni scenari, invece, Windows PowerShell rappresenta il modo più efficiente o addirittura l'unico modo per eseguire un'attività di gestione. Ad esempio, l'interfaccia di amministrazione di Skype for Business online consente di personalizzare gli inviti alle riunioni:

![Impostazioni delle convocazioni di riunione dell'Interfaccia di amministrazione di Lync](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Impostazioni delle convocazioni di riunione dell'Interfaccia di amministrazione di Lync")

Le stesse personalizzazioni possono essere eseguite mediate il cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md), ma il **Set-CsMeetingConfiguration** include anche opzioni non disponibili nell'interfaccia di amministrazione di Skype for Business online. Ad esempio, se una persona nell'organizzazione partecipa a una riunione, viene configurata automaticamente come relatore per impostazione predefinita. Questa impostazione non può essere modificata mediante l'interfaccia di amministrazione di Skype for Business online, ma solo usando Windows PowerShell e il cmdlet **Set-CsMeetingConfiguration**. In particolare, questo comando imposta la proprietà DesignateAsPresenter su None, che significa che solo l'organizzatore della riunione verrà configurato come relatore quando partecipa alla riunione:

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

Per informazioni dettagliate sull'uso di Windows PowerShell, vedere gli argomenti seguenti:

  - [Cmdlet, parametri e valori di parametro di Windows PowerShell](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [Uso di parametri](working-with-parameters-in-skype-for-business-online.md)

  - [Parametri obbligatori e facoltativi](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [Parametri e proprietà](parameters-vs-properties-in-skype-for-business-online.md)

  - [Combinazione di cmdlet di Lync Online con altri cmdlet di Windows PowerShell](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [Informazioni utili per l'uso di Windows PowerShell](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

