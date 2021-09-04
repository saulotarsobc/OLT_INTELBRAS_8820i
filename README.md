# OLT GPON INTELBRAS 8820i

## 🚧 EM CONSTRUÇÃO

## ⚠️ versão de firmware da olt: 2.76 ⚠️

![image](https://user-images.githubusercontent.com/23584038/128234027-a7dff4e8-0073-4a24-a47e-f7d147b4a312.png)

## O que vai encontrar nesse template?

- SISTEMA
  - UPTIME
  - MEMORIA RAM LIVRE
  - CPU
- STATUS DAS PORTAS
- GPON
  - STATUS DA GPON
  - CORRENTE
  - VOLTAGEM
  - CONTADOR DE ONU's POR PON
  - RX POWER
  - TX POWER
  - TEMPERATURA

[Video demo](/contents/demo.mp4)

[Template](./contents/OLT_INTELBRAS_8820i.xml)

[Dashboard](contents/OLT_INTELBRAS_8820i.xml)

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

> Contador de ONU's Online por PON.

```js
$.[?(@.PON == '1' && @.ACT == '1')].length()
$.[?(@.PON == '2' && @.ACT == '1')].length()
$.[?(@.PON == '3' && @.ACT == '1')].length()
...
```

> Contador de ONU's Provisionadas por PON.

```js
$.[?(@.PON == '1' && @.REG == '1')].length()
$.[?(@.PON == '2' && @.REG == '1')].length()
$.[?(@.PON == '3' && @.REG == '1')].length()
...
```
![image](https://user-images.githubusercontent.com/23584038/132105625-24060a34-e00d-4880-8bc3-02b6eeb9cdd4.png)
