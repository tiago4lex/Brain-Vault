2025-09-09 23:12

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[AnonSurf]] | [[Ferramentas]]

----
# Introdução

O **AnonSurf** é uma ferramenta incluída que permite redirecionar **todo o tráfego da rede do sistema operacional através da rede Tor**.

Diferente de apenas abrir o **Tor Browser**, que  protege apenas a navegação dentro do navegador, o AnonSurf força que **todas as conexões de aplicativos** (navegadores, terminais, clientes de e-mail, etc.) passem pela rede Tor.

Assim, o usuário consegue garantir **anonimato e privacidade** em um nível mais profundo cobrindo praticamente todo o sistema operacional.

![[Pasted image 20250909231605.png]]

---
# Como o AnonSurf funciona?

O AnonSurf trabalha basicamente em três etapas:

1. **Redirecionamento de tráfego:** cria regras no `iptables` para forçar todas as conexões a passarem pelo serviço Tor.
2. **Configuração do DNS:** evita vazamento de DNS *(DNS Leaks)*, redirecionando consultas também pela rede Tor.
3. **Gestão de Serviço:** oferece comandos simples para iniciar, para reiniciar o modo anônimo.

Na prática, ao ativar o AnonSurf, o **IP de saída da máquina muda constantemente,** conforme os nós da rede Tor são trocados.

---
# Comandos principais do AnonSurf

No terminal, os comandos seguem a sintaxe:

```bash
anonsurf <comando>
```

### Comandos mais usados

- `anonsurf start`: Ativa o redirecionamento de todo o tráfego via Tor.
- Exemplo:

```bash
sudo anonsurf start
```

Depois disso, qualquer site verá um IP diferente do real, fornecido pela rede Tor.

- Exemplo:

```bash
sudo anonsurf stop
```

- `anonsurf restart`: Reinicia o serviço, útil se houver falhas na conexão Tor.
- `anonsurf status`: Exibe o estado atual do AnonSurf (ativado, desativado ou em erro).
- `anonsurf change`: Troca de identidade Tor, mudando o IP de saída sem reiniciar o serviço.
- Exemplo:

```bash
sudo anonsurf change
```

- Útil quando o site bloqueia seu nó atual.
- `anonsurf myip`: Mostra o endereço IP que está sendo exibido externamente (via Tor).
- Exemplo:

```bash
anonsurf myip
```

- `anonsurf service`: Gerencia manualmente o serviço Tor, útil para troubleshooting.

---
# Exemplos de Cenários de Uso

### ### 🧪 1. Testes de anonimato

Um analista de cibersegurança pode ativar o AnonSurf antes de visitar sites suspeitos ou honeypots, evitando expor o IP real.

### 🌍 2. Acesso a conteúdos bloqueados

Em países com censura na internet, o AnonSurf permite contornar bloqueios e acessar informações livremente.

### 🔍 3. Coleta de informações em OSINT

Durante investigações de **Inteligência de Ameaças (Threat Intelligence)** ou **OSINT**, o AnonSurf ajuda a proteger a identidade do analista ao navegar em fóruns, redes sociais ou dark web.

### 💻 4. Simulações em pentest

Durante um teste de intrusão, o pentester pode usar AnonSurf para mascarar o tráfego de rede e não revelar o IP da empresa contratada.

---
# Vantagens e Desvantagens

### ✅ Vantagens:

- **Anonimato total do tráfego** (não apenas do navegador).
- **Prevenção de DNS leaks** por padrão.
- **Facilidade de uso** com comandos simples.
- Integração nativa no **Parrot Security OS**.
- Útil em contextos de **cibersegurança defensiva e ofensiva**.

### ❌ Desvantagens:

- **Velocidade da rede reduzida** (a rede Tor é naturalmente lenta).
- Alguns sites bloqueiam acessos vindos de nós Tor.
- **Não substitui boas práticas de segurança**: se o usuário se identificar em um site (ex: logar com e-mail pessoal), o anonimato é quebrado.
- Pode gerar **alertas em investigações forenses** (trafegar sempre via Tor pode chamar atenção de monitoramentos).

---
# AnonSurf na Cibersegurança

Na prática, o AnonSurf é usado em diferentes áreas:

- **Pentest e Red Team:**  
    → Mascarar conexões durante exploração de vulnerabilidades, dificultando rastreamento.
    
- **OSINT (Open Source Intelligence):**  
    → Navegar em fontes abertas (clara e dark web) sem revelar o IP real.
    
- **Blue Team / Defensiva:**  
    → Testar como a rede da empresa reage a conexões anônimas.
    
- **Privacidade pessoal:**  
    → Proteger a identidade ao usar redes públicas ou acessar conteúdos sensíveis.

---
# Diferença entre AnonSurf e TorSocks

## 1. AnonSurf

- Ferramenta exclusiva do **Parrot Security OS**.    
- **Força todo o tráfego do sistema** (navegadores, terminais, programas, etc.) a passar pela rede Tor.
- Usa **iptables** para redirecionar conexões.
- Vem com proteções extras contra **DNS leaks**.
- É **global** → qualquer aplicativo que use a internet vai sair com IP Tor.

- Exemplo:

```bash
sudo anonsurft start
```

Depois disso, mesmo que você abra o Firefox normal ou um cliente de e-mail, o tráfego sairá pela rede Tor.

## 2. TorSocks

- Ferramenta independente, funciona em qualquer Linux com Tor instalado.
- Usada para rodar **aplicativos específicos** através da rede Tor.
- Não força todo o tráfego do sistema → apenas o do programa que você iniciar com `torsocks`.
- Mais granular: você escolhe **qual app** usar com Tor.
- Útil quando você quer proteger só um processo, sem afetar o resto do sistema.

- Exemplo:

```bash
torsocks curl ifconfig.me
```

Isso retorna o IP de saída pela rede Tor, mas apenas o **curl** foi forçado a usar Tor.  
Se você abrir o Firefox fora do torsocks, ele não será anonimizado.

## 3. Comparação lado a lado

| Característica    | **AnonSurf**                          | **TorSocks**                                              |
| ----------------- | ------------------------------------- | --------------------------------------------------------- |
| Escopo            | Todo o sistema                        | Apenas um processo/app                                    |
| Implementação     | iptables + Tor + redirecionamento DNS | LD_PRELOAD para redirecionar chamadas de rede             |
| Facilidade de uso | Ativa/desativa com 1 comando          | Precisa prefixar cada app com `torsocks`                  |
| Risco de leaks    | Menor (protege DNS globalmente)       | Maior (se esquecer de usar torsocks, o tráfego vai limpo) |
| Performance       | Mais lento (tudo passa pelo Tor)      | Mais rápido (só apps específicos usam Tor)                |
| Casos de uso      | Anonimato total do sistema            | Testar/usar apenas um app de forma anônima                |

## 4. Cenários de Uso

- **AnonSurf**  
	- Pesquisador de OSINT navegando em múltiplos navegadores + clientes de rede.  
	- Pentester que quer mascarar **todo o sistema** durante testes de intrusão.  
	- Usuário que deseja **anonimato total** em qualquer aplicação, sem risco de esquecer de usar Tor.
    
- **TorSocks**  
	- Desenvolvedor que precisa testar apenas um script Python ou curl com tráfego Tor.  
	- Usuário que quer rodar apenas um cliente IRC/SSH com anonimato, sem lentificar o resto do sistema.  
	- Quando você **não quer** que todo o tráfego do PC passe pelo Tor (ex: atualizações de pacotes que precisam sair pelo IP real).

---
# Conclusão

O **AnonSurf** é uma poderosa ferramenta para quem busca **anonimato completo do sistema operacional**, indo além do simples uso do Tor Browser.  
É ideal para pesquisadores de segurança, pentesters e profissionais que lidam com dados sensíveis, mas deve ser usado com consciência, pois **anonimato ≠ invulnerabilidade**.