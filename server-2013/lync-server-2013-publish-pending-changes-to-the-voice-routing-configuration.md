---
title: "Lync Server 2013: Pubblica modifiche in sospeso a configuraz. routing vocale"
TOCTitle: Pubblicare le modifiche in sospeso alla configurazione del routing vocale
ms:assetid: ff941d0b-fb4b-47d2-b866-6d990ac66b81
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413088(v=OCS.15)
ms:contentKeyID: 49302590
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-07_

Dopo aver apportato modifiche alle impostazioni di configurazione nelle pagine del gruppo **Routing vocale** , eseguire questa procedura per esaminare, pubblicare o annullare le modifiche in sospeso.

> [!IMPORTANT]  
> Verificare che un solo utente alla volta modifichi le impostazioni di configurazione di Routing vocale.<br />Tutte le modifiche in sospeso devono essere pubblicate contemporaneamente eseguendo il comando <strong>Salva tutto</strong> . Non è possibile pubblicare selettivamente le modifiche in sospeso. Prima di pubblicare le modifiche in sospeso, eseguire il comando <strong>Rivedi modifiche di cui non è stato eseguito il commit</strong> e annullare qualsiasi modifica di configurazione che non si desidera pubblicare.<br />Se si esce dalle pagine del gruppo <strong>Routing vocale</strong> prima di eseguire il commit delle modifiche in sospeso, tutte le modifiche in sospeso andranno perse. Tuttavia, è possibile esportare la configurazione corrente (incluse le modifiche in sospeso) in un file di configurazione vocale e quindi importare e pubblicare la configurazione aggiornata. Per informazioni dettagliate, vedere <a href="lync-server-2013-export-a-voice-route-configuration-file.md">Esportare un file di configurazione di route vocali in Lync Server 2013</a>.

## Per rivedere, pubblicare o annullare le modifiche di configurazione del routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** .

4.  Apportare le modifiche della configurazione desiderate alle impostazioni in ogni pagina del gruppo **Routing vocale** .

5.  Per rivedere le modifiche in sospeso senza pubblicarle, scegliere **Rivedi modifiche di cui non è stato eseguito il commit** dal menu **Commit** .

6.  Se si desidera annullare qualsiasi modifica in sospeso, effettuare una delle operazioni seguenti:
    
      - Scegliere **Annulla tutte le modifiche di cui non è stato eseguito il commit** dal menu **Commit** .
    
      - Spostarsi sulla scheda della pagina **Routing vocale** che include le modifiche in sospeso che si desidera annullare, selezionare l'elemento con le modifiche in sospeso, fare clic su **Commit** e quindi su **Annulla modifiche selezionate** .

7.  Dopo aver rivisto tutte le modifiche in sospeso e annullato ogni modifica che non si desidera pubblicare, fare clic su **Commit** e quindi su **Salva tutto** .

8.  Nella finestra di dialogo **Impostazioni di configurazione vocale di cui non è stato eseguito il commit** in cui è visualizzato un elenco delle modifiche in sospeso fare clic su **OK** .
    
    Dopo che Pannello di controllo di Lync Server esegue il commit delle modifiche, viene visualizzato il messaggio **Configurazione di routing vocale pubblicata correttamente** .

