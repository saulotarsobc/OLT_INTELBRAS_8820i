# OLT GPON INTELBRAS 8820i

## 🚧 Atualizando para a versão de firmware 2.81

## ATIVE AS NOTIFICAÇÕES PARA FICAR LIGADO NAS NOVIDADES

![image](https://user-images.githubusercontent.com/23584038/132106564-72ab4986-3c8a-4074-9d0b-9bc77e5c9d80.png)

## ⚠️ versão de firmware da olt: 2.81 ⚠️

![image](https://user-images.githubusercontent.com/23584038/128234027-a7dff4e8-0073-4a24-a47e-f7d147b4a312.png)

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

[Dashboard](contents/grafana_dash_OLT_INTELBRAS_8820i.json)

## ZABBIX - TEMPLATE

> Dividi o Template em quatro. Para usar conforme a necessidade.

![image](https://user-images.githubusercontent.com/23584038/132104647-9a10ebe3-7e61-4314-ad9b-a80b87942411.png)

> O descoberta para analise de trafego filtra apenas as interfaces com status UP.

```js
discovery[{#NAME},1.3.6.1.4.1.26138.1.1.1.1.1.2, {#STATUS},1.3.6.1.2.1.2.2.1.8]
```

> Item discovery de ONU's. Busca se as ONU's estão autorizadas, online e qual é a PON.

```js
discovery[{#PON},1.3.6.1.4.1.26138.1.2.1.1.1.2, {#ACT},1.3.6.1.4.1.26138.1.2.1.1.1.5, {#REG}, 1.3.6.1.4.1.26138.1.2.1.1.1.4]
```

> Pré-processamento

![image](https://user-images.githubusercontent.com/23584038/132104637-16ef4efd-9108-498a-b0b9-34216717acb7.png)


> Contador de ONU's Provisionadas por PON.

```js
1.3.6.1.4.1.26138.1.4.1.1.1.56.9 = reg.pon1
1.3.6.1.4.1.26138.1.4.1.1.1.56.10 = reg.pon2
1.3.6.1.4.1.26138.1.4.1.1.1.56.11 = reg.pon3
1.3.6.1.4.1.26138.1.4.1.1.1.56.12 = reg.pon4
1.3.6.1.4.1.26138.1.4.1.1.1.56.13 = reg.pon5
1.3.6.1.4.1.26138.1.4.1.1.1.56.14 = reg.pon6
1.3.6.1.4.1.26138.1.4.1.1.1.56.15 = reg.pon7
1.3.6.1.4.1.26138.1.4.1.1.1.56.16 = reg.pon8
```

> Contador de ONU's Ativas por PON.

```js
1.3.6.1.4.1.26138.1.4.1.1.1.55.9 = act.pon1
1.3.6.1.4.1.26138.1.4.1.1.1.55.10 = act.pon2
1.3.6.1.4.1.26138.1.4.1.1.1.55.11 = act.pon3
1.3.6.1.4.1.26138.1.4.1.1.1.55.12 = act.pon4
1.3.6.1.4.1.26138.1.4.1.1.1.55.13 = act.pon5
1.3.6.1.4.1.26138.1.4.1.1.1.55.14 = act.pon6
1.3.6.1.4.1.26138.1.4.1.1.1.55.15 = act.pon7
1.3.6.1.4.1.26138.1.4.1.1.1.55.16 = act.pon8
...
```

> Contador de ONU's Offline por PON. (Item calculado)

```js
onus.off.pon1 = last("reg.pon1")/last("act.pon1")
onus.off.pon2 = last("reg.pon2")/last("act.pon2")
onus.off.pon3 = last("reg.pon3")/last("act.pon3")
onus.off.pon4 = last("reg.pon4")/last("act.pon4")
onus.off.pon5 = last("reg.pon5")/last("act.pon5")
onus.off.pon6 = last("reg.pon6")/last("act.pon6")
onus.off.pon7 = last("reg.pon7")/last("act.pon7")
onus.off.pon8 = last("reg.pon8")/last("act.pon8")
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

![image](https://user-images.githubusercontent.com/23584038/132105625-24060a34-e00d-4880-8bc3-02b6eeb9cdd4.png)
