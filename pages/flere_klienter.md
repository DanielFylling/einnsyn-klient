---
title: Flere einnsyn-klienter på samme integrasjonspunkt
description: Flere einnsyn-klienter på samme integrasjonspunkt
summary: "Her finner du informasjon om hvordan bruke flere einnsyn-klienter på samme integrasjonspunkt"
permalink: flere_klienter.html

layout: page
sidebar: main_sidebar
---

Når du skal bruke flere integrasjonspunkt eller einnsyn-klienter på samme server må du bruke forskjellige porter. Om du skal bruke ett integrasjonspunkt og flere einnsyn-klienter må du endre id, navn og port på einnsyn-klient tjenesten. I tillegg må hver einnsyn-klient ha sin egen inputDirectory-mappe. 
Alt dette endres i einnsyn-klient.xml-filen. I tillegg må du legge til et ekstra argument:

* ```-Dserver.port= ```

Om du skal ha flere integrasjonspunkt installert på samme server må du endre server.port i integrasjonspunkt-local.properties for hver instans. Denne må være unik. Du må også da peke ```-Dapplication.moveUrl=``` til å gå mot riktig integrasjonspunkt og port. Porten som integrasjonspunktet og einnsyn-klienten trenger ikke være like. 


``` java
<service>
      <id>einnsyn-klient-2</id> Her må du ha unik ID for prosessen
      <name>einnsyn-klient-2</name> Dette namnet blir det som viser i lista over windows tjenester.
      <description>Klient for parsing og sending av journaldata</description>
      <env name="USE_IP" value="true"/>
      <env name="RECEIVER_ORGNUMMER" value="991825827" />
      <argument>-jar</argument>
      <argument>-Dapplication.moveUrl=</argument> Denne må være unik. Forteller hvilket integrasjonspunkt den kobler til http://localhost:9093 94, 95...
      <argument>-Dapplication.inputDirectory=</argument>
      <argument>-Dapplication.orgnummer=</argument> 
      <argument>-Dserver.port=</argument> Her setter du egen port for denne einnsyn-klienten. For eksempel 9094, 9095, 9096…
      <argument>-Dspring.mail.host=</argument>
      <argument>-Dspring.mail.port</argument>
      <argument>-Dspring.mail.username=</argument>
      <argument>-Dspring.mail.password=</argument>
      <argument>sender-2017-11-29T10_48.jar</argument>
      <logpath>%BASE%/logs</logpath>
      <executable>javaw</executable>
</service>
```

[Her kan du laste ned einnsyn-klient.xml-filen](..resources/avansert/einnsyn-klient.xml)
