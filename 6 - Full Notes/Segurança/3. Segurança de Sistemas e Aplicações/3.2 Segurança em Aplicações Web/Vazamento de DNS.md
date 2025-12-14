2025-08-12 15:02

Status: #developed #segurança 

Tags:[[CyberSecurity]] | [[DNS]]

----
# Introdução

## O que é Vazamento de DNS?

**Vazamento de DNS *(DNS Leak)*** ocorre quando consultas de DNS (Domain Name System) escapam de uma conexão criptografada (como VPT, Tor ou Proxy) e são enviadas em texto clara para o servidor DNS padrão do provedor de internet (ISP). Isso expõe os sites que você visita, mesmo que você esteja usando ferramentas de privacidade.

![[Pasted image 20250812150539.png]]

## Impactos de um Vazamento de DNS

- Seu ISP ou atacantes podem ver quais sites você acessa.
- Perda de anonimato ao usar VPN/TOR.
- Exposição de atividades sensíveis (navegação privada, pentesting).

---
# Como Funciona o Vazamento de DNS?

Quando você digita `google.com` no navegador, seu sistema precisa resolver o nome para um IP. Se o DNS não estiver devidamente protegido, a consulta pode vazar:

1. **Sem VPN/TOR:**
	- Consulta DNS → ISP DNS (vazamento claro).

2. **Com VPN/TOR (mas com vazamento):**
	- Consulta DNS → **ISP DNS** (em vez do DNS da VPN/TOR)

3. **Conexão Correta (sem vazamento):**
	- Consulta DNS → **Servidor DNS da VPN/TOR** (protegido)

---
# Causas comuns de Vazamento de DNS

## a) Configuração Incorreta de VPN/Proxy

- Se a VPN não redirecionar o tráfego DNS corretamente, seu sistema usará o DNS padrão (ISP).

## b) IPv6 não bloqueado

- Muitas VPNs não manipulam IPv6, permitindo vazamentos.

## c) Sistema Operacional Enviando Consultas Alternativas

- Windows 10+ usa DNS **over HTTPS (DoH)** ou **LLMNR/NBT-NS**, que podem ignorar a VPN.

## d) Aplicativos Ignorando a VPN

- Navegadores como Firefox podem usar **DNS próprio** (ex.: Cloudflare DoH).

---
# Como verificar se há Vazamento de DNS?

## Método 1: Usando Sites de Teste

- [DNSLeakTest.com](https://dnsleaktest.com)
- [IPLeak.net](https://ipleak.net)

### Resultado Esperado (VPN ativa):

- Os servidores DNS listados devem pertencer à sua VPN (não ao seu ISP).

### Resultados com Vazamento:

- Aparecem servidores do seu ISP (ex.: `Claro DNS`, `Vivo DNS`).

## Método 2: Via Terminal (Linux/macOS)

```bash
dig +short myip.opendns.com @resolver1.opendns.com # verifica IP
dig +short google.com              # verifica qual dns respondeu
```

Se o IP/DNS não corresponder à sua VPN, há vazamento.

---
# Como evitar Vazamento de DNS?

## a) Usando VPNs Confiáveis (Com Kill Switch)

- **ProtonVPN, Mullvad, NordVPN** bloqueiam DNS leaks por padrão.

## b) Forçar DNS da VPN

**No Windows**:

1. `Configurações > Rede e Internet > Adaptador de Rede`.
2. Clique com o botão direito na VPN → Propriedades > IPv4.
3. Defina DNS manualmente (ex.: `1.1.1.1` , `8.8.8.8`).

**No Linux (via `resolv.conf`):**

```bash
sudo echo "nameserver 1.1.1.1" > /etc/resolv.conf && chattr +i /etc/resolv.conf
```

## c) Evitar IPv6

**No Linux:**

```bash
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
```

**No Windows:**

1. `Painel de Controle > Redes > Adaptadores de Rede`.
2. Desmarque **"Protocolo IP Versão 6(TCP/IPv6)"**.

## d) Navegadores usando DNS Criptografado

- **Firefox**: Ative **DNS over HTTPS (DoH)** em: `Configurações > Geral > Configurações de Rede > Ativar DoH`.

## e) Usando TOR (o melhor para anonimato)

```bash
torsoccks firefox # Navegação anônima com DNS via TOR
```

---
# Exemplos de Vazamento de DNS em ataques reais

## Cenário 1: Pentester Usando VPN com Vazamento

- Um hacker é rastreável porque seu Kali Linux usou o DNS da Claro, não da VPN.

## Cenário 2: Usuário da Dark Web exposto

- Consultas DNS para `.onion` vazaram para o ISP, quebrando o anonimato.

---
# Ferramentas para Detectar e Prevenir Vazamentos

| **Ferramenta**     | **Uso**                            |
| ------------------ | ---------------------------------- |
| Wireshark          | Analisa pacotes DNS em tempo real. |
| dnscrypt-proxy     | Criptografa consultas DNS.         |
| Kill Switch (VPNs) | Bloqueia tráfego se a VPN cair.    |

---
# Conclusão

Vazamentos de DNS são uma falha crítica de privacidade. Para se proteger:

✅ **Use VPNs com Kill Switch**
✅ **Force DNS criptografado (DoH/DoT)**
✅ **Desative IPv6**
✅ **Monitore vazamentos regularmente**

>[!note] **Dica Final:**
>Sempre teste sua conexão após configurar uma VPN/TOR!


