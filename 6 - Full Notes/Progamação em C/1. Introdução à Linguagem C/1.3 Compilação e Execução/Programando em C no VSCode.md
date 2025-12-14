2025-08-19 08:22

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[VSCode]]

----
# 1. Instalar o VSCode

Se ainda não tiver, baixe e instale o [Visual Studio Code](https://code.visualstudio.com/).

---
# 2. Instalar o Compilador de C

O VSCode não vem com um compilador embutido, então é necessário instalar um.

## No Windows

- Baixe e instale o [MinGW-w64](https://www.mingw-w64.org/downloads/).
- Durante a instalação, selecione:
    - **Architecture:** x86_64
    - **Threads:** win32
    - **Exception:** `seh`

- Depois de instalado, adicione `C:\Program Files\mingw-w64\mingw64\bin` ao **PATH** do sistema.

## No Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install build-essential
```

## No MacOS:

Instale o **Xcode Command Line Tools**:

```bash
xcode-select --install
```

---
# 3. Instalar a Extensão C/C++

No VSCode:

1. Vá até a aba **Extensões** (`Ctrl + Shift + X`).
2. Pesquise por **C/C++** e instale a extensão da Microsoft.

![[Pasted image 20250819082635.png]]

---
# 4. Criar e rodar um Código em C

1. Crie um novo arquivo `main.c` e escreva um código simples:

```c
#include <stdio.h>

int main() {
	printf("Hello World!\n");
	return 0;
}
```

2. **Compilar e Executar manualmente**  no terminal:

	- **No Windows:**

	```sh
gcc main.c -o main.exe
.\main.exe
	```

	- No Linux/macOS:

```bash
gcc main.c -o main
./main
```

