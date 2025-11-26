# Estruturas Condicionais e de Repetição

## 🎯 O que eu aprendi

Identação e blocos de comando, estruturas condicionais (if, elif, else), estruturas de repetição (for, while) e suas variantes, essenciais para controlar o fluxo de programas em Python.

---

## 🔧 Identação e Blocos de Comando

### O que é Identação?

**Identação** é a prática de adicionar espaços no início das linhas para organizar o código visualmente e, em Python, para definir blocos de código.

**Em Python, a identação é obrigatória!**

O interpretador usa a identação para entender onde cada bloco começa e termina.

### Convenção: 4 Espaços

Python recomenda usar **4 espaços** para cada nível de identação:

```python
# Nível 0 (sem identação)
if idade >= 18:
    # Nível 1 (4 espaços)
    print("Maior de idade")
    if saldo > 0:
        # Nível 2 (8 espaços)
        print("Pode fazer saque")
```

### ⚠️ Erro Comum: Misturar Tabs e Espaços

```python
# ❌ ERRADO (misturando tabs e espaços)
if x > 0:
→ print("positivo")  # Tab aqui
    print("continua")  # Espaços aqui
# IndentationError!

# ✅ CORRETO
if x > 0:
    print("positivo")  # 4 espaços
    print("continua")  # 4 espaços
```

---

## ❓ Estruturas Condicionais

São comandos que permitem tomar decisões no código baseado em condições específicas.

### **if - Condição Simples**

```python
idade = 20

if idade >= 18:
    print("Você é maior de idade")
```

**O bloco dentro do if só executa se a condição for `True`.**

### **else - Alternativa**

```python
idade = 15

if idade >= 18:
    print("Maior de idade")
else:
    print("Menor de idade")  # Vai executar isso
```

### **elif - Múltiplas Condições**

Use `elif` (else if) para testar várias condições em sequência:

```python
nota = 7.5

if nota < 6:
    print("❌ Reprovado")
elif nota < 7:
    print("⚠️ Recuperação")
else:
    print("✅ Aprovado")
```

**Como funciona:**
1. Python testa a primeira condição (`nota < 6`)
2. Se for falsa, testa a segunda (`nota < 7`)
3. Se também for falsa, executa o `else`
4. Assim que uma condição for verdadeira, o bloco executa e as demais são ignoradas

### **Importante: elif é Opcional**

```python
# Pode ter 0, 1 ou vários elif
if x > 10:
    print("Muito grande")
elif x > 5:
    print("Grande")
elif x > 0:
    print("Pequeno")
else:
    print("Negativo ou zero")
```

---

## 🔄 If Aninhado (if dentro de if)

Um `if` dentro de outro `if`, para testar condições dependentes:

```python
idade = 25
tem_carteira = True

if idade >= 18:
    print("Maior de idade")
    if tem_carteira:
        print("Pode dirigir!")  # Só executa se AMBAS forem verdadeiras
    else:
        print("Precisa tirar carteira")
```

---

## ⚡ If Ternário (Uma Linha)

Forma compacta para uma condição simples:

```python
# Formato: valor_se_verdade if condicao else valor_se_falso
status = "Aprovado" if nota >= 7 else "Reprovado"

# Equivalente a:
# if nota >= 7:
#     status = "Aprovado"
# else:
#     status = "Reprovado"
```

**Recomendação:** Use if ternário para decisões simples. Use if/elif/else para decisões complexas.

---

## 🔁 Estruturas de Repetição

Comandos que repetem um bloco de código várias vezes.

### **for - Iterar Sequências Conhecidas**

Ideal quando você sabe exatamente quantas vezes vai repetir (ou qual coleção vai percorrer).

```python
# Exemplo 1: Iterar uma lista
frutas = ["maçã", "banana", "laranja"]
for fruta in frutas:
    print(fruta)
# Saída:
# maçã
# banana
# laranja

# Exemplo 2: Iterar números
for i in range(1, 4):
    print(i)
# Saída: 1, 2, 3
```

### **Função range()**

Gera uma sequência de números inteiros.

```python
# range(stop) - do 0 até stop-1
range(5)  # 0, 1, 2, 3, 4

# range(start, stop) - de start até stop-1
range(1, 5)  # 1, 2, 3, 4

# range(start, stop, step) - com passo
range(0, 10, 2)  # 0, 2, 4, 6, 8

# Para ver os valores, converta em lista:
list(range(5))  # [0, 1, 2, 3, 4]
```

### **Exemplo: Tabuada do 5**

```python
for numero in range(0, 21, 5):
    print(numero, end=" ")
# Saída: 0 5 10 15 20
```

### **while - Repetir Enquanto Condição for Verdadeira**

Útil quando não sabe exatamente quantas repetições (mas conhece a condição de parada).

```python
contador = 0
while contador < 3:
    print(f"Contagem: {contador}")
    contador += 1
# Saída:
# Contagem: 0
# Contagem: 1
# Contagem: 2
```

### **while True - Loop Infinito com Condição de Parada**

```python
while True:
    numero = input("Digite um número (ou 'sair' para parar): ")
    if numero.lower() == "sair":
        break
    print(f"Você digitou: {numero}")
```

---

## 🛑 break - Sair do Loop

Interrompe a repetição imediatamente:

```python
for numero in range(10):
    if numero == 5:
        break  # Para quando numero é 5
    print(numero)
# Saída: 0, 1, 2, 3, 4
```

---

## ⏭️ continue - Pular Iteração

Pula a iteração atual e vai para a próxima:

```python
# Imprimir apenas números pares
for numero in range(10):
    if numero % 2 != 0:
        continue  # Pula números ímpares
    print(numero, end=" ")
# Saída: 0 2 4 6 8
```

---

## 📚 for/else e while/else

O `else` executa quando o loop termina normalmente (sem `break`):

```python
# Exemplo: Buscar número em lista
numeros = [1, 3, 5, 7]
procurando = 2

for numero in numeros:
    if numero == procurando:
        print("Encontrado!")
        break
else:
    print("Não encontrado")  # Executa porque o loop terminou sem break
```

**Nota:** `for/else` e `while/else` são pouco usados no dia a dia.

---

## 💡 Exemplos Práticos para Data Science

### **Exemplo 1: Classificar Risco**

```python
risco = 0.75  # Métrica de risco

if risco < 0.3:
    classificacao = "Baixo risco"
elif risco < 0.6:
    classificacao = "Médio risco"
else:
    classificacao = "Alto risco"

print(f"Classificação: {classificacao}")
```

### **Exemplo 2: Processar Lista de Dados**

```python
dados = [10, 20, 15, 30, 5]
total = 0

for valor in dados:
    if valor > 10:
        total += valor

print(f"Soma dos valores > 10: {total}")  # 95
```

### **Exemplo 3: Validação com while**

```python
entrada_valida = False

while not entrada_valida:
    idade = input("Digite sua idade: ")
    if idade.isdigit() and int(idade) > 0:
        entrada_valida = True
        print(f"Você tem {idade} anos")
    else:
        print("Entrada inválida. Digite um número positivo.")
```

---

## ⚠️ Erros Comuns

```python
# ❌ ERRO: Esquecer identação
if x > 0:
print("positivo")  # SyntaxError!

# ✅ CORRETO
if x > 0:
    print("positivo")

# ❌ ERRO: Usar = em vez de ==
if nome = "Maria":  # SyntaxError
    pass

# ✅ CORRETO
if nome == "Maria":
    pass

# ❌ ERRO: Loop infinito sem condição de parada
while True:
    x += 1
    # Nunca sai!

# ✅ CORRETO
while x < 10:
    x += 1
```

---

## 🎯 Resumo de Estruturas

| Estrutura | Quando Usar | Exemplo |
|-----------|------------|---------|
| **if** | Uma condição simples | `if age >= 18:` |
| **if/else** | Duas opções | `if x > 0: / else:` |
| **if/elif/else** | Múltiplas opções | `if / elif / elif / else` |
| **if ternário** | Uma linha, condição simples | `"Sim" if x else "Não"` |
| **for** | Iterar sequência conhecida | `for item in lista:` |
| **while** | Repetir até condição | `while x < 10:` |
| **break** | Sair do loop | `if x == 5: break` |
| **continue** | Pular iteração | `if x % 2: continue` |

---

## 🔗 Recursos Recomendados

- [Documentação Python - if statements](https://docs.python.org/pt-br/3/tutorial/controlflow.html#if-statements)
- [Documentação Python - for loops](https://docs.python.org/pt-br/3/tutorial/controlflow.html#for-statements)
- [Documentação Python - while loops](https://docs.python.org/pt-br/3/reference/compound_stmts.html#while)

---

[⬅️ Voltar ao Índice do Módulo](README.md)