
---
# Introdução

O projeto **Casa Inteligente com Estrutura de Árvore** tem como objetivo demonstrar a aplicação de **estrutura de dados** (mais especificamente, **árvores compostas por nós**), em um contexto prático de **automação residencinal** usando o **Arduino UNO**.

Cada cômodo da casa é representado como um **nó folha** de uma estrutura de árvore, e a **casa** (raiz da árvore) contém ponteiros para esses nós. O sistema permite ligar e desligar LEDs (simbolizando lâmpadas) por meio de botões físicos, com feedback exibido no ***Serial Monitor***.

---
# Estrutura de Dados

## Estrutura `Comodo`

A estrutura `Comodo` representa cada **nó folha** da árvore.

Cada cômodo possui:

```cpp
struct Comodo {
	String nome;
	int pinoLed;
	int pinoBotao;
	bool habilitado.
	bool estaAceso;
	int ultimoEstadoBotao;
	unsigned long ultimoTempoDebounce;
};
```

**Explicação dos Campos:**

| Atributo              | Função                                                                 |
| --------------------- | ---------------------------------------------------------------------- |
| `nome`                | Nome do cômodo (ex.: "Sala", "Cozinha").                               |
| `pinoLed`             | Pino digital conectado ao LED do cômodo.                               |
| `pinoBotao`           | Pino digital conectado ao botão.                                       |
| `habilitado`          | Indica se o cômodo está ativo.                                         |
| `estaAceso`           | Define se o LED está ligado (true) ou desligado (false).               |
| `ultimoEstadoBotao`   | Armazena o último estado lido do botão, usado para **debounce**.       |
| `ultimoTempoDebounce` | Marca o tempo da última leitura estável, também usado no **debounce**. |

>[!note] Nota:
>*Debounce* é uma técnica para evitar leituras falsas quando o botão é pressionado, devido a pequenos ruídos elétricos.

## Estrutura `Casa`

A estrutura `Casa` é o **nó raiz da árvore**. Ela mantém um array de ponteiros para os cômodos:

```cpp
struct Casa {
	String nome;
	Comodo* comodos[4];
	int numComodos;	
};
```

**Função dos Atributos**

| Atributo     | Descrição                                        |
| ------------ | ------------------------------------------------ |
| `nome`       | Identifica a raiz (por exemplo, "Raiz da Casa"). |
| `comodos[4]` | Vetor de ponteiros para os nós `Comodo`.         |
| `numComodos` | Indica quantos nós (cômodos) estão conectados.   |

Assim, a relação entre os elementos pode ser visualizada como:

```
           Casa (Raiz)
         /  |       |  \
	    /   |       |   \
	   /    |       |    \
   Sala  Cozinha Quarto  Banheiro
```

Cada cômodo é um **nó folha** conectado à raiz.

---
# Inicialização e Estruturação da Árvore

A função `inicializarEstrutura()` é responsável por **criar e conectar os nós**:

```cpp
void inicializarEstrutura() {
	minhaCasa.nome = "Raiz da Casa";
	minhaCasa.numComodos = 4;
	
	for (int i =0; i < minhaCasa.numComodos; i++) {
		Comodo* novoComodo = new Comodo; // Alocação Dinâmica
		...
		minhaCasa.comodos[i] = novoComodo;
	}
}
```

**Conceitos Importantes:**

- O uso do `new` realiza **alocação dinâmica de memória**, criando cada cômodo em tempo de execução.
- Cada ponteiro `minhaCasa.comodos[i]` **aponta** para um `Comodo`n a memória.
- Isso simula a **estrutura hierárquica** de uma árvore.

---
# Configuração de Hardware

Após criar a estrutura lógica, o Arduino configura os pinos físicos na função `inicializarPinos()`:

```cpp
void inicializarPinos() {
	for (int i = 0; i < minhaCasa.numComodos; i++) {
		Comodo* c = minhaCasa.comodos[i];
		pinMode(c->pinoLed, OUTPUT);
		pinMode(c->pinoBotao, INPUT_PULLUP);
	}
}
```

- Cada LED é configurado como **saída digital** (`OUTPUT`).
- Cada botão é configurado como `INPUT_PULLUP`, usando o resistor interno do Arduino. Isso significa que o botão estará em **HIGH** quando solto e **LOW** quando pressionado.

---
# Função `loop()`: Percorrendo a Árvore

A função `loop()` percorre todos os nós da árvore repetidamente, verificando se houve alguma mudança:

```cpp
for (int i = 0; i < minhaCasa.numComodos; i++) {
	Comodo* comodoAtual = minhaCasa.comodos[i];
	if (processarBotao(comodoAtual)) {
		estadoGeralMudou = true;
	}
	atualizarLed(comodoAtual);
}
```

Isso é análogo a percorrer uma **árvore em profundidade**, onde cada nó (cômodo) é visitado para:

- Processar o estado do botão;
- Atualizar o estado do LED correspondente.

---
# Função `processarBotao()`: Lógica com Debaunce

```cpp
bool processarBotao(Comodo* c) {
	int leitura = digitalRead(c->pinoBotao);
	if (leitura != c->ultimoEstadoBotao) {
		if (millis() - c->ultimoTempoDebounce > DEBOUNCE_DELAY) {
			if (leitura == LOW) {
				c->estaAceso = !c->estaAceso;
			}
			c->ultimoEstadoBotao = leitura;
			c->ultimoTempoDebounce = millis();
		}
	}
	return estadoMudou;
}
```

**Resumo da lógica:**

1. Detecta mudança no estado do botão.
2. Verifica se o tempo mínimo de debounce passou (50 ms).
3. Alterna o estado lógico de LED (`estaAceso`).
4. Atualiza o tempo e o último estado.

Essa função retorna `true` se o estado do cômodo mudou, permitindo que o sistema atualiza o relatório.

---
# Função `atualizarLed()`

```cpp
void atualizarLed(Comodo* c) {
	if (c->habilitado && c->estaAceso)
		digitalWrite(c->pinoLed, HIGH);
	else
		digitalWrite(c->pinoLed, LOW);
}
```

Essa função **reflete o estado lógico do nó (`estaAceso)` no hardware físico** (LED ligado/desligado).

---
# Função `imprimirStatus()`

Responsável por exibir no ***Serial Monitor*** o status atual da árvore:

```cpp
void imprimirStatus() {
	for (int i = 0; i < minhaCasa.numComodos; i++) {
		Comodo* c = minhaCasa.comodos[i];
		Serial.print(c->nome);
		Serial.print(c->estaAceso ? " ACESA" : " APAGADA");
	}
}
```

O resultado é uma visão geral da "casa":

```text
=========================================
  RELATÓRIO DE STATUS DA CASA (ÁRVORE)
=========================================
Sala (Pino 2): ACESA
Cozinha (Pino 3): APAGADA
Quarto (Pino 4): APAGADA
Banheiro (Pino 5): APAGADA
-----------------------------------------
Total de Cômodos: 4 | LEDs Acesos: 1
-----------------------------------------
```

---
# Conclusão

Este projeto une conceitos teóricos e práticos:

- **Estruturas de dados:** implementação de uma árvore com alocação dinâmica.
- **Programação orientada a objetos (C estrutural):** uso de structs e ponteiros.
- **Interação com hardware:** controle físico de LEDs e botões via pinos digitais.
- **Boas práticas:** uso de `debounce`, relatórios no monitor serial e modularização por funções.