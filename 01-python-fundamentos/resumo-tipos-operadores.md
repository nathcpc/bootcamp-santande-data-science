# Tipos de Operadores com Python

## 🎯 O que aprendi

Todos os tipos de operadores em Python e como usá-los em expressões.

---

## ➕ Operadores Aritméticos

São as contas matemáticas.

| Operador | Nome | Descrição | Exemplo | Resultado |
|----------|------|-----------|---------|-----------|
| `+` | Adição | Soma dois valores | `5 + 3` | `8` |
| `-` | Subtração | Subtrai dois valores | `5 - 3` | `2` |
| `*` | Multiplicação | Multiplica dois valores | `5 * 3` | `15` |
| `/` | Divisão | Divide e retorna float | `5 / 2` | `2.5` |
| `//` | Divisão Inteira | Divide e retorna int | `5 // 2` | `2` |
| `%` | Módulo | Retorna o resto | `5 % 2` | `1` |
| `**` | Potência | Elevado a potência | `5 ** 2` | `25` |

### Exemplos Práticos

```python
# Adição e Subtração
saldo = 100
saque = 30
novo_saldo = saldo - saque  # 70

# Multiplicação
preco_unitario = 10.50
quantidade = 3
total = preco_unitario * quantidade  # 31.50

# Divisão e Divisão Inteira
total_reais = 100
num_pessoas = 3
por_pessoa = total_reais / num_pessoas      # 33.333...
por_pessoa_inteira = total_reais // num_pessoas  # 33

# Módulo (resto da divisão)
idade = 25
resto = idade % 5  # 0 (25 é divisível por 5)
eh_par = 10 % 2    # 0 (se for 0, é par)

# Potência
resultado = 2 ** 10  # 1024
resultado = 9 ** 0.5  # 3.0 (raiz quadrada)
```

---

## 🔄 Operadores de Atribuição

Usados para atribuir valores a variáveis.

| Operador | Exemplo | Equivalente |
|----------|---------|-------------|
| `=` | `x = 5` | Atribui valor |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `//=` | `x //= 3` | `x = x // 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `**=` | `x **= 3` | `x = x ** 3` |

### Exemplos

```python
# Atribuição simples
x = 10

# Atribuição com operação
x += 5   # x agora é 15 (x = x + 5)
x -= 3   # x agora é 12 (x = x - 3)
x *= 2   # x agora é 24 (x = x * 2)
x /= 4   # x agora é 6.0 (x = x / 4)

# Atribuição múltipla
a, b, c = 1, 2, 3  # a=1, b=2, c=3

# Swap (trocar valores)
a, b = b, a  # Troca os valores de a e b
```

---

## 🔍 Operadores de Comparação

Usados para comparar valores. Retornam `True` ou `False`.

| Operador | Descrição | Exemplo | Resultado |
|----------|-----------|---------|-----------|
| `==` | Igual | `5 == 5` | `True` |
| `!=` | Diferente | `5 != 3` | `True` |
| `>` | Maior que | `5 > 3` | `True` |
| `<` | Menor que | `5 < 3` | `False` |
| `>=` | Maior ou igual | `5 >= 5` | `True` |
| `<=` | Menor ou igual | `5 <= 3` | `False` |

### Exemplos Práticos

```python
idade = 25
limite = 18

# Comparações numéricas
idade > limite          # True
idade < limite          # False
idade == 25             # True
idade != 30             # True
idade >= limite         # True

# Comparações com strings
nome = "Python"
nome == "Python"        # True
nome != "Java"          # True

# Comparações em condições
if idade >= limite:
    print("Maior de idade")  # Será executado
else:
    print("Menor de idade")

# Comparação com booleanos
ativo = True
ativo == True           # True
ativo != False          # True
```

---

## 🧠 Operadores Lógicos

Usados para combinar condições. Retornam `True` ou `False`.

| Operador | Descrição | Exemplo | Resultado |
|----------|-----------|---------|-----------|
| `and` | E lógico (ambos True) | `True and True` | `True` |
| `or` | OU lógico (um True) | `True or False` | `True` |
| `not` | NÃO lógico (inverte) | `not True` | `False` |

AND para ser True tudo tem que ser TRUE /
OR para ser TRUE apenas um tem que ser TRUE

### Tabela de Verdade

```
AND:
True  and True   = True
True  and False  = False
False and True   = False
False and False  = False

OR:
True  or True    = True
True  or False   = True
False or True    = True
False or False   = False

NOT:
not True         = False
not False        = True
```

### O Truque para Lembrar
`AND (E)`: Pense em critérios que TODOS devem passar

"Para viajar: tenho que ter passaporte E dinheiro E férias aprovadas"

`OR (OU)`: Pense que só UMA coisa precisa acontecer

"Vou ao trabalho usando ônibus OU carro OU bicicleta" (só precisa de um)

`NOT (NÃO)`: Pense em inverter

"NÃO está chovendo" = o contrário de "está chovendo"

### Exemplos Práticos

```python
idade = 25
tem_carteira = True
tem_carro = False

# AND - Ambas as condições devem ser verdadeiras
pode_dirigir = (idade >= 18) and (tem_carteira)  # True

# OR - Pelo menos uma deve ser verdadeira
pode_sair = (tem_carro) or (tem_carteira)  # True

# NOT - Inverte o resultado
nao_pode_dirigir = not pode_dirigir  # False

# Combinando operadores
if (idade >= 18) and (tem_carteira) and tem_carro:
    print("Pode dirigir para viajar!")
else:
    print("Não pode viajar de carro")

# Com variáveis
salario = 5000
tem_poupanca = True
pode_comprar = (salario > 3000) and tem_poupanca  # True
```

---

## 🔗 Operadores de Associação e Identidade

### Operadores de Associação (`in`, `not in`)

Verificam se um valor está em uma sequência.

```python
# IN - Verifica se está na sequência
frutas = ["maçã", "banana", "laranja"]
"maçã" in frutas         # True
"uva" in frutas          # False

# NOT IN - Verifica se NÃO está
"uva" not in frutas      # True
"banana" not in frutas   # False

# Com strings
texto = "Python"
"P" in texto             # True
"xyz" in texto           # False

# Em condições
if "admin" in ["user", "moderator", "admin"]:
    print("Tem acesso!")
```

### Operadores de Identidade (`is`, `is not`)

Sao utilizados para comparar se os dois objetos testados usam a mesma posição na memória. 
Ou seja: verificam se dois objetos são o MESMO objeto (não só iguais).

```python
# IS - Mesmo objeto na memória
a = [1, 2, 3]
b = [1, 2, 3]
c = a

a == b              # True (conteúdo igual)
a is b              # False (objetos diferentes)
a is c              # True (mesmo objeto)

# Com None
valor = None
valor is None       # True
valor is not None   # False
```

---

## 📊 Precedência de Operadores

Ordem em que os operadores são executados (do maior para menor precedência):

```python
# Operações com mesma precedência são executadas da esquerda para direita

# 1º: Parênteses
resultado = (5 + 3) * 2  # 16 (não 11)

# 2º: Potência
resultado = 2 + 3 ** 2   # 11 (3² = 9, depois 2 + 9)

# 3º: Multiplicação, Divisão, Módulo (esquerda para direita)
resultado = 10 / 2 * 5   # 25 (não 1)

# 4º: Adição, Subtração (esquerda para direita)
resultado = 10 - 5 + 3   # 8 (não 2)

# 5º: Comparações
resultado = 5 > 3 and 2 < 4  # True

# 6º: Lógico NOT
resultado = not 5 > 3    # False

# 7º: Lógico AND
resultado = True and False or True  # True

# 8º: Lógico OR
resultado = False or False or True  # True
```

---

## 💡 Exemplos de Expressões Complexas

```python
# 1. Idade com AND
idade = 25
tem_carteira = True
pode_dirigir = (idade >= 18) and tem_carteira  # True

# 2. Número válido
numero = 42
eh_positivo = numero > 0
eh_menor_100 = numero < 100
valido = eh_positivo and eh_menor_100  # True

# 3. Status de acesso
admin = False
moderador = True
usuario = False
tem_acesso = admin or moderador  # True

# 4. Validação de dados
salario = 5000
tem_poupanca = True
pode_emprestar = (salario >= 3000) and (salario <= 10000) and tem_poupanca  # True

# 5. Com NOT
bloqueado = False
pode_acessar = not bloqueado  # True
```

---

## ⚠️ Erros Comuns

```python
# ❌ ERRO: usar = em comparação
if idade = 18:       # SyntaxError
    pass

# ✅ CORRETO: usar ==
if idade == 18:
    pass

# ❌ ERRO: misturar and/or sem clareza
resultado = True or False and False  # Confuso!

# ✅ CORRETO: usar parênteses
resultado = (True or False) and False  # Claro!

# ❌ ERRO: comparar strings com números
"5" > 3              # TypeError: '>' not supported between str and int

# ✅ CORRETO: converter tipos
int("5") > 3         # True
```

---

## 🎯 Resumo de Operadores

```python
# Aritméticos: + - * / // % **
# Atribuição: = += -= *= /= //= %= **=
# Comparação: == != > < >= <=
# Lógicos: and or not
# Associação: in not in
# Identidade: is is not
```

---

## 🔗 Recursos Recomendados

- [Documentação Python - Operators](https://docs.python.org/pt-br/3/reference/lexical_analysis.html#operators)
- [Precedência de Operadores](https://docs.python.org/pt-br/3/reference/expressions.html#operator-precedence)

---

[⬅️ Voltar ao Índice do Módulo](README.md)
