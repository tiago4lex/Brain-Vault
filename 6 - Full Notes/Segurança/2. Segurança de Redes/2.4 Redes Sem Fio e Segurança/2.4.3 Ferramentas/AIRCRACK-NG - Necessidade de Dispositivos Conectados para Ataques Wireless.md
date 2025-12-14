2025-09-03 15:35

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wi-Fi]]

----
# Introdução

A necessidade de dispositivos conectados varia significativamente entre diferentes tipos de ataques wireless. Alguns ataques **exigem** clientes conectados, enquanto outros podem ser realizados **sem nenhum cliente ativo**.

---
# Visão Geral por Tipo de Ataque

## 1. Ataques que REQUEREM dispositivos conectados

- Ataques **WPA/WPA2-PSK *(Handshake Capture)***
	- **Porquê:** Necessitam capturar o "4-way handshake" de autenticação.
	- **Clientes necessários:** Pelo menos 1 dispositivo conectado.

- **Ataques de Deautenticação**
	- **Propósito:** interromper serviço ou forçar reassociação.
	- **Clientes necessários:** Pelo menos 1 para ataques específicos.

- **Ataques ARP Replay (WEP)**
	- **Propósito:** Gerar tráfego para coletar IVs.
	- **Clientes necessários:** Pelo menos 1 dispositivo ativo.

## 2. Ataques que NÃO REQUEREM dispositivos conectados

- **Ataques WEP (Passivo)**
	- **Funcionamento:** Coleta passiva de IVs ao longo do tempo.
	- **Clientes necessários:** 0 (mas é extremamente lento).

- **Ataques PMKID (WPA/WPA2)**
	- **Inovação:** Captura PMKID do ponto de acesso sem handshake.
	- **Clientes necessários:** 0 (ataque diretamente ao AP).

- **Ataques a WPS *(Wi-Fi Protected Setup)***
	- **Alvo:** Vulnerabilidade no protocolo WPS do AP.
	- **Clientes necessários:** 0 (ataque diretamente ao AP).

- **Ataques a Redes Ocultas (SSID)**
	- **Técnica:** Monitorar frames de reassociação.
	- **Cliente necessários:** 0 (mas requer que clientes se conectem eventualmente).

---
# Estratégias para Redes sem Clientes Conectados

## 1. Criar Clientes Artificiais

### Evil Twin Attack

```bash
# Criar AP falso com mesmo SSID
sudo airbase-ng -a [BSSID] --essid "[SSID]" -c [CHANNEL] wlan0mon

# Esperar que clientes se conectem automaticamente
```

### KARMA Attack

**Conceito:** Responder a qualquer probe request.

```bash
# Usando hostpad com KARMA
sudo hostapd karma.conf
```

## 2. Ataques Passivos de Longa Duração

### Captura de Handshake em Background

```bash
# Captura continua esperando handshake
sudo airodump-ng -c [CHANNEL] --bssid [BSSID] -w long_capture --write-interval 10 wlan0mon
```

### Monitoramento de Beacon Frames

```bash
# Analisar informações mesmo sem clientes
sudo airodump-ng wlan0mon --band abg
```

---
# Impacto do Número de Clientes na Eficiência

## 1. Ataques WEP

| **Cenário**        | **IVs/Minuto** | **Tempo Estimado** |
| ------------------ | -------------- | ------------------ |
| Sem clientes       | 5-20           | 50-200 horas       |
| 1 cliente inativo  | 10-50          | 20-100 horas       |
| 1 cliente ativo    | 100-500        | 2-10 horas         |
| 5+ clientes ativos | 1000-5000      | 5-30 minutos       |

## 2. Captura de Handshake WPA

| **Cenário**         | **Probabilidade de Sucesso** | **Tempo**   |
| ------------------- | ---------------------------- | ----------- |
| Sem clientes        | 0%                           | ♾️          |
| 1 cliente conectado | 80%                          | 2-5 minutos |
| 5+ clientes         | 90%                          | <1 minuto   |

---
# Implicações para Segurança

## 1. Para Administradores de Rede

**Recomendações:**

- Monitorar tentativas de deautenticação.
- Implementar proteção contra ataques WPS.
- Usar WPA3 quando possível (resistente a ataque PMKID).
- Desativar WPS se não for necessário.

## 2. Para Testes de Penetração

**Estratégia:**

- Priorizar redes com clientes conectados.
- Para redes sem clientes: usar ataques PMKID ou WPS.
- Considerar ataques de evil twin para atrair clientes.
- Planejar testes em horários de pico de uso.

---
