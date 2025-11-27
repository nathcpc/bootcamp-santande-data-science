# Dominando Funções em Python

## 🎯 O que eu aprendi

Como criar funções profissionais, utilizar argumentos avançados (*args e **kwargs), entender escopo e aplicar conceitos fundamentais para Data Science.

---

## 📋 O que é uma Função?

Uma **função** é um bloco de código reutilizável que realiza uma tarefa específica. Em Python, funções são definidas com a palavra-chave `def`.

**Por que usar?**
- ✅ **Reutilização:** Escreva uma vez, use várias vezes.
- ✅ **Organização:** Divide problemas complexos em partes menores.
- ✅ **Manutenção:** Fácil de corrigir e melhorar.

```python
def saudacao(nome):
    return f"Olá, {nome}!"

print(saudacao("Maria"))  # Olá, Maria!
```

---

## 🔄 Retornando Valores (`return`)

Toda função em Python retorna algo. Se você não especificar, ela retorna `None` implicitamente.

### **Retorno Simples**

```python
def somar(a, b):
    return a + b

resultado = somar(10, 5)  # 15
```

### **Retorno Múltiplo (Tuplas)**

Python permite retornar vários valores de uma vez (muito útil em Data Science para retornar, por exemplo, dados de treino e teste).

```python
def estatisticas(lista):
    media = sum(lista) / len(lista)
    total = sum(lista)
    return media, total  # Retorna uma tupla

valores = [10, 20, 30]
media, total = estatisticas(valores)  # Desempacotamento

print(f"Média: {media}, Total: {total}")
```

---

## 🎯 Tipos de Argumentos

### **Posicionais vs Nomeados**

```python
def criar_carro(marca, modelo, ano):
    return f"{marca} {modelo} ({ano})"

# Posicional (ordem importa)
print(criar_carro("Fiat", "Uno", 2010))

# Nomeado (ordem não importa)
print(criar_carro(ano=2022, marca="Tesla", modelo="Model 3"))

# Misto (posicionais devem vir antes)
print(criar_carro("Ford", ano=2020, modelo="Ka"))
```

### **Valores Padrão (Default)**

Torna argumentos opcionais.

```python
def conectar_banco(host="localhost", porta=5432):
    return f"Conectando em {host}:{porta}"

print(conectar_banco())                 # Conectando em localhost:5432
print(conectar_banco("192.168.1.5"))    # Conectando em 192.168.1.5:5432
```

---

## 📦 Args e Kwargs (Argumentos Variáveis)

Essenciais quando você não sabe quantos argumentos serão passados (ex: funções de bibliotecas como Pandas e Matplotlib usam muito isso).

### **`*args` (Tupla de Argumentos)**
Recebe múltiplos argumentos posicionais como uma **tupla**.

```python
def somar_tudo(*args):
    return sum(args)

print(somar_tudo(1, 2, 3, 4))  # 10
print(somar_tudo(10, 20))      # 30
```

### **`**kwargs` (Dicionário de Argumentos)**
Recebe múltiplos argumentos nomeados como um **dicionário**.

```python
def configurar_modelo(**kwargs):
    for parametro, valor in kwargs.items():
        print(f"Configurando {parametro}: {valor}")

configurar_modelo(learning_rate=0.01, epochs=100, optimizer="adam")
# Saída:
# Configurando learning_rate: 0.01
# Configurando epochs: 100
# Configurando optimizer: adam
```

### **Combinando Tudo**

```python
def treinar_modelo(dados, *args, **kwargs):
    print(f"Dados: {dados}")
    print(f"Args extras: {args}")
    print(f"Configurações: {kwargs}")
```

---

## 🔒 Parâmetros Especiais (`/` e `*`)

Você pode forçar como os argumentos devem ser passados.

```python
# / -> Tudo antes DEVE ser posicional
# * -> Tudo depois DEVE ser nomeado

def funcao_rigida(pos1, pos2, /, nomeado1, *, nomeado2):
    print(pos1, pos2, nomeado1, nomeado2)

# Exemplo de uso obrigatório
funcao_rigida(10, 20, nomeado1=30, nomeado2=40)
```

---

## 🌍 Escopo de Variáveis (Local vs Global)

- **Local:** Variável criada dentro da função (só existe lá).
- **Global:** Variável criada fora (acessível em todo lugar).

```python
salario = 5000  # Global

def calcular_bonus():
    bonus = 500  # Local
    return salario + bonus  # Pode ler global

print(calcular_bonus())  # 5500
# print(bonus)  # Erro! 'bonus' não existe aqui fora
```

**⚠️ Cuidado:** Evite usar `global` para modificar variáveis externas dentro de funções. Isso torna o código difícil de testar e manter (efeito colateral).

---

## 🚀 Funções como Objetos de Primeira Classe

Em Python, funções são objetos. Você pode:
1. Atribuir função a uma variável
2. Passar função como argumento para outra
3. Retornar função de outra função

**Exemplo em Data Science:**
Passar uma função de limpeza para ser aplicada em uma coluna.

```python
def limpar_texto(texto):
    return texto.strip().lower()

dados = ["  Python  ", "  DATA SCIENCE  "]

# map aplica a função em cada item
dados_limpos = list(map(limpar_texto, dados))
print(dados_limpos)  # ['python', 'data science']
```

---

## ⚡ Funções Anônimas (Lambda)

Funções pequenas, de uma linha, sem nome. Muito usadas com `filter()`, `map()` e em DataFrames Pandas.

**Sintaxe:** `lambda argumentos: expressao`

```python
somar = lambda x, y: x + y
print(somar(2, 3))  # 5

# Uso prático: Ordenar lista pelo tamanho da string
nomes = ["Ana", "Carlos", "Bia"]
nomes.sort(key=lambda nome: len(nome))
print(nomes)  # ['Ana', 'Bia', 'Carlos']
```

---

## 📊 Exemplo Prático: Pipeline de Dados

```python
def carregar_dados():
    return [10, 20, 30, None, 50]

def limpar_dados(lista):
    # Remove valores nulos (None)
    return [x for x in lista if x is not None]

def normalizar(lista):
    maximo = max(lista)
    return [x / maximo for x in lista]

def pipeline():
    dados = carregar_dados()
    dados_limpos = limpar_dados(dados)
    dados_finais = normalizar(dados_limpos)
    return dados_finais

resultado = pipeline()
print(resultado)  # [0.2, 0.4, 0.6, 1.0]
```

---

## 🔗 Recursos Recomendados

- [Documentação Python - Funções](https://docs.python.org/pt-br/3/tutorial/controlflow.html#defining-functions)
- [PEP 8 - Guia de Estilo para Funções](https://peps.python.org/pep-0008/#function-names)

---

[⬅️ Voltar ao Índice do Módulo](README.md)