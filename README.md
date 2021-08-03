# OLT GPON INTELBRAS 8820i

## ⏳ Em contruçao... ⚡

![image](https://user-images.githubusercontent.com/23584038/127940755-d5691f16-95eb-464d-89b5-604860610a87.png)

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

![image](https://user-images.githubusercontent.com/23584038/128022449-86581802-1282-4ebc-a16e-efbaae2cd852.png)

> Item discovery de ONU's. Busca a se as ONU's estão autorizadas e qual é a PON.

```js
discovery[{#REG},1.3.6.1.4.1.26138.1.2.1.1.1.4, {#PON},1.3.6.1.4.1.26138.1.2.1.1.1.2]
```
> Pré-processamento

![image](https://user-images.githubusercontent.com/23584038/128008078-2a86115e-44ba-4e8f-8213-b50a2963d803.png)

> Contador de ONU's ativas por PON.

```js
$.[?(@.PON == '1' && @.REG == '1')].length()
$.[?(@.PON == '2' && @.REG == '1')].length()
$.[?(@.PON == '3' && @.REG == '1')].length()
$.[?(@.PON == '4' && @.REG == '1')].length()
$.[?(@.PON == '5' && @.REG == '1')].length()
$.[?(@.PON == '6' && @.REG == '1')].length()
$.[?(@.PON == '7' && @.REG == '1')].length()
$.[?(@.PON == '8' && @.REG == '1')].length()
```
