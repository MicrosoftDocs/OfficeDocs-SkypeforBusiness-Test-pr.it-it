---
title: Visualizzazione delle informazioni sul profilo dei criteri di larghezza di banda della rete
TOCTitle: Visualizzazione delle informazioni sul profilo dei criteri di larghezza di banda della rete
ms:assetid: eed453fc-04e9-4971-959c-6fad54bf1c96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721931(v=OCS.15)
ms:contentKeyID: 49887814
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sul profilo dei criteri di larghezza di banda della rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Nel servizio Controllo di ammissione di chiamata (CAC) viene utilizzato un criterio di larghezza di banda per definire le limitazioni della larghezza di banda per alcune modalità. In Microsoft Lync Server 2013, è possibile assegnare tali limitazioni solo alle modalità audio e video. È possibile impostare limitazioni della larghezza di banda globali o per le sessioni. È possibile utilizzare il Pannello di controllo di Lync Server per creare, modificare o eliminare un profilo contenitore per tali criteri. Ogni profilo di criteri della larghezza di banda può essere associato a uno o più siti di rete. Utilizzare le procedure seguenti per visualizzare un profilo di criteri della larghezza di banda. Per creare o modificare un profilo di criteri della larghezza di banda, vedere [Creazione o modifica di profili di criteri di larghezza di banda](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md).

## Per modificare un profilo di criteri della larghezza di banda

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri larghezza di banda**.

4.  Nella pagina **Criteri larghezza di banda** fare clic sul profilo di criteri della larghezza di banda che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

## Visualizzazione di informazioni relative a un profilo di criteri della larghezza di banda di rete tramite cmdlet di PowerShell per Lync Server

È possibile visualizzare i profili della larghezza di banda di rete anche utilizzando il cmdlet Get-CsNetworkBandwidthPolicyProfile di PowerShell per Lync Server. Questo cmdlet può essere eseguito in Lync Server 2013 Management Shell o in una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione di informazioni relative a un profilo di criteri della larghezza di banda di rete

  - Per visualizzare informazioni su tutti i profili di criteri della larghezza di banda di rete, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsNetworkBandwidthPolicyProfile
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity          : RedmondBandwidthPolicy
        BWPolicy          : {BWLimit=200;BWSessionLimit=200;
                            BWPolicyModality=Audio, 
                            BWLimit=1400;BWSessionLimit=500;
                            BWPolicyModality=Video}
        BWPolicyProfileID : RedmondBandwidthPolicy
        Description       :

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Get-CsNetworkBandwidthPolicyProfile](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkBandwidthPolicyProfile).

## Vedere anche

#### Attività

[Creazione o modifica di profili di criteri di larghezza di banda](lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md)  
[Eliminazione dei profili criteri larghezza di banda della rete](lync-server-2013-deleting-network-bandwidth-policy-profiles.md)  

#### Ulteriori risorse

[Configurare il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-call-admission-control.md)

