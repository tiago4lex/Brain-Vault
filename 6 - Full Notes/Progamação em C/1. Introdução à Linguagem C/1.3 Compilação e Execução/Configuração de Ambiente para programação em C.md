2025-05-05 12:06

Status: #developed #C

Tags: [[Programação em C]] | [[C]] 

----
# Conceito Geral

### **Instalar o Compilador de C**

O VSCode não vem com um compilador embutido, então você precisa instalar um.

#### **No Windows:**

- Baixe e instale o MinGW-w64.
    
- Durante a instalação, selecione:
    
    - **Architecture:** x86_64
        
    - **Threads:** win32
        
    - **Exception:** seh
        
- Depois de instalado, adicione `C:\Program Files\mingw-w64\mingw64\bin` ao **PATH** do sistema.

#### **No Linux (Ubuntu/Debian):**

`sudo apt update sudo apt install build-essential`

#### **No MacOS:**

Instale o **Xcode Command Line Tools**:

`xcode-select --install`

### 3. **Instalar a Extensão C/C++**

No VSCode:

1. Vá até a aba **Extensões** (`Ctrl + Shift + X`).
    
2. Pesquise por **C/C++** e instale a extensão da Microsoft.
    

### 4. **Criar e Rodar um Código em C**

1. Crie um novo arquivo `main.c` e escreva um código simples:
    
    `#include <stdio.h>`  
    `int main() {     
		`printf("Hello, World!\n");     
		`return 0; 
	`}
    
2. **Compilar e executar manualmente** no terminal:
    
    - No Windows:
        
        `gcc main.c -o main.exe .\main.exe`
        
    - No Linux/macOS:
        
        `gcc main.c -o main ./main`

----


