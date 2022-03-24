# OLT GPON INTELBRAS 8820i

## 🚧 Atualizando para a versão de firmware 2.81

## ATIVE AS NOTIFICAÇÕES PARA FICAR LIGADO NAS NOVIDADES

![image](https://user-images.githubusercontent.com/23584038/132106564-72ab4986-3c8a-4074-9d0b-9bc77e5c9d80.png)

## ⚠️ versão de firmware da olt: 2.81 ⚠️

## Apoio

[Zabbix Documentation 5.4 - Itens calculados](https://www.zabbix.com/documentation/5.4/pt/manual/config/items/itemtypes/calculated)

![image](https://user-images.githubusercontent.com/23584038/128234027-a7dff4e8-0073-4a24-a47e-f7d147b4a312.png)

[Dashboard](contents/grafana_dash_OLT_INTELBRAS_8820i.json)

## Zabbix Templates

- [Zabbix 5.0](contents/OLT_INTELBRAS_8820i_ONUs%20zabbix%205_0.xml)

- [Zabbix 5.4](contents/OLT_INTELBRAS_8820i_ONUs%20zabbix%205_4.xml)

## O que vai encontrar nesses templates?

- SISTEMA
  - UPTIME
  - MEMORIA RAM LIVRE
  - CPU
  - TEMPERATURA
  
- STATUS DAS PORTAS

- GPON
  - STATUS DA GPON
  - CORRENTE
  - VOLTAGEM
  - CONTADOR DE ONU's POR PON
    - ONLINE
    - OFFLINE
  - RX POWER
  - TX POWER
  - TEMPERATURA

[Video demo](/contents/demo.mp4)

## ZABBIX - TEMPLATE

> Dividi o Template em quatro. Para usar conforme a necessidade

![image](https://user-images.githubusercontent.com/23584038/132104647-9a10ebe3-7e61-4314-ad9b-a80b87942411.png)

> O descoberta para analise de trafego filtra apenas as interfaces com status UP

```js
discovery[{#NAME},1.3.6.1.4.1.26138.1.1.1.1.1.2, {#STATUS},1.3.6.1.2.1.2.2.1.8]
```

> Monitoramento geral

```js
cpuUsage 1.3.6.1.4.1.2021.11.9.0 (%)
memTotal 1.3.6.1.4.1.2021.4.5.0 (KB)
memFree 1.3.6.1.4.1.2021.4.6.0 (KB)
uptime 1.3.6.1.2.1.1.3.0 (uptime)
systemStatusSensor1Temperature 1.3.6.1.4.1.26138.1.5.1.1.0 (°C)
systemStatusSensor2Temperature 1.3.6.1.4.1.26138.1.5.1.2.0 (°C)
```

> Contador de ONU's Provisionadas por PON

```js
TOTAL REGISTRADAS PON X
reg[pon1]

1.3.6.1.4.1.26138.1.4.1.1.1.56.9
reg[pon2]

1.3.6.1.4.1.26138.1.4.1.1.1.56.10
reg[pon3]

1.3.6.1.4.1.26138.1.4.1.1.1.56.11
reg[pon4]

1.3.6.1.4.1.26138.1.4.1.1.1.56.12
reg[pon5]

1.3.6.1.4.1.26138.1.4.1.1.1.56.13
reg[pon6]

1.3.6.1.4.1.26138.1.4.1.1.1.56.14
reg[pon7]

1.3.6.1.4.1.26138.1.4.1.1.1.56.15
reg[pon8]

1.3.6.1.4.1.26138.1.4.1.1.1.56.16
```

> Contador de ONU's Ativas por PON

```js
TOTAL ATIVAS PON X
act[pon1]
1.3.6.1.4.1.26138.1.4.1.1.1.55.9

act[pon2]
1.3.6.1.4.1.26138.1.4.1.1.1.55.10

act[pon3]
1.3.6.1.4.1.26138.1.4.1.1.1.55.11

act[pon4]
1.3.6.1.4.1.26138.1.4.1.1.1.55.12

act[pon5]
1.3.6.1.4.1.26138.1.4.1.1.1.55.13

act[pon6]
1.3.6.1.4.1.26138.1.4.1.1.1.55.14

act[pon7]
1.3.6.1.4.1.26138.1.4.1.1.1.55.15

act[pon8]
1.3.6.1.4.1.26138.1.4.1.1.1.55.16
```

> Contador de ONU's Offline por PON. (Item calculado)

```js
TOTAL INATIVAS PON X
onus.inac.pon1
last("reg.pon1")-last("act.pon1")

onus.inac.pon2
last("reg.pon2")-last("act.pon2")

onus.inac.pon3
last("reg.pon3")-last("act.pon3")

onus.inac.pon4
last("reg.pon4")-last("act.pon4")

onus.inac.pon5
last("reg.pon5")-last("act.pon5")

onus.inac.pon6
last("reg.pon6")-last("act.pon6")

onus.inac.pon7
last("reg.pon7")-last("act.pon7")

onus.inac.pon8
last("reg.pon8")-last("act.pon8")
```

![image](https://user-images.githubusercontent.com/23584038/132105625-24060a34-e00d-4880-8bc3-02b6eeb9cdd4.png)
