# Utilizando Dicionários em Python

## 🎯 O que eu aprendi

Como criar, acessar e manipular dicionários, a estrutura chave-valor fundamental para trabalhar com dados JSON e configurações em Data Science.

---

## 📋 O que é um Dicionário?

Um **dicionário** é uma coleção **não ordenada** de pares **chave: valor**.

**Características:**
- ✅ **Mapeamento:** Associa uma chave única a um valor.
- ✅ **Chaves únicas e imutáveis:** A chave não pode se repetir e deve ser imutável (string, número, tupla).
- ✅ **Mutável:** O dicionário em si pode ser alterado (adicionar/remover itens).

```python
# Criando dicionários
pessoa = {"nome": "Maria", "idade": 28}
vazio = {}
construtor = dict(nome="João", idade=30)

print(pessoa)  # {'nome': 'Maria', 'idade': 28}
```

---

## 🔍 Acessando Valores

### **Acesso Direto (Colchetes)**
Se a chave não existir, gera erro `KeyError`.

```python
pessoa = {"nome": "Maria", "idade": 28}

print(pessoa["nome"])  # Maria
# print(pessoa["email"]) # KeyError!
```

### **Método `.get()` (Seguro)**
Se a chave não existir, retorna `None` (ou um valor padrão) sem dar erro.

```python
print(pessoa.get("nome"))           # Maria
print(pessoa.get("email"))          # None
print(pessoa.get("email", "Vazio")) # "Vazio" (valor padrão)
```

---

## 🏗️ Dicionários Aninhados

Dicionários dentro de dicionários. Muito comum em estruturas JSON e APIs.

```python
contatos = {
    "maria@email.com": {"nome": "Maria", "telefone": "1234-5678"},
    "joao@email.com": {"nome": "João", "telefone": "9999-9999"}
}

# Acessando valores profundos
telefone_maria = contatos["maria@email.com"]["telefone"]
print(telefone_maria)  # 1234-5678
```

---

## 🔄 Iterar Dicionários

### **1. Iterar Chaves (Padrão)**
```python
for chave in pessoa:
    print(chave)  # nome, idade
```

### **2. Iterar Valores (`.values()`)**
```python
for valor in pessoa.values():
    print(valor)  # Maria, 28
```

### **3. Iterar Itens (`.items()`) - Mais Útil!**
Retorna chave e valor ao mesmo tempo (como tuplas).

```python
for chave, valor in pessoa.items():
    print(f"{chave}: {valor}")
# nome: Maria
# idade: 28
```

---

## 🛠️ Métodos Importantes da Classe `dict`

| Método | O que faz | Exemplo |
|--------|-----------|---------|
| `.keys()` | Retorna todas as chaves | `d.keys()` |
| `.values()` | Retorna todos os valores | `d.values()` |
| `.items()` | Retorna lista de tuplas (chave, valor) | `d.items()` |
| `.clear()` | Apaga tudo | `d.clear()` |
| `.copy()` | Cópia superficial | `novo = d.copy()` |
| `.fromkeys()` | Cria dict com chaves e valor padrão | `dict.fromkeys(["a","b"], 0)` |
| `.get(k, v)` | Busca valor (retorna v se não achar) | `d.get("chave", "padrão")` |
| `.pop(k)` | Remove chave e retorna valor | `valor = d.pop("nome")` |
| `.popitem()` | Remove o último item adicionado | `chave, valor = d.popitem()` |
| `.setdefault()` | Se chave não existe, adiciona com valor | `d.setdefault("idade", 0)` |
| `.update()` | Atualiza/Mescla dicionários | `d.update(novo_dict)` |

### Exemplos Práticos

```python
# fromkeys - Inicializar contadores
chaves = ["a", "b", "c"]
dict_inicial = dict.fromkeys(chaves, 0)
print(dict_inicial)  # {'a': 0, 'b': 0, 'c': 0}

# setdefault - Adicionar se não existir
pessoa = {"nome": "Maria"}
pessoa.setdefault("idade", 18)  # Adiciona idade: 18
pessoa.setdefault("nome", "Ana") # Não muda (já existe)
print(pessoa)  # {'nome': 'Maria', 'idade': 18}

# update - Mesclar dicionários
infos_extras = {"cidade": "SP", "nome": "Maria Silva"}
pessoa.update(infos_extras)
print(pessoa)  # {'nome': 'Maria Silva', 'idade': 18, 'cidade': 'SP'}
```

---

## 🗑️ Remover Itens (`del`)

Podemos usar a palavra-chave `del`.

```python
dados = {"a": 1, "b": 2}

del dados["a"]
print(dados)  # {'b': 2}

# del dados["z"]  # KeyError se não existir!
```

---

## 🕵️ Verificar Existência (`in`)

Forma elegante de checar se uma chave existe.

```python
contato = {"nome": "Maria", "email": "maria@email.com"}

if "email" in contato:
    print(f"Email: {contato['email']}")
else:
    print("Sem email cadastrado")
```

---

## 📊 Dicionários em Data Science

Dicionários são a base para trabalhar com **JSON** e **Pandas**.

### **DataFrame a partir de Dicionário**
No Pandas, é muito comum criar DataFrames (tabelas) a partir de dicionários:

```python
# Exemplo (conceitual)
dados = {
    "Nome": ["Maria", "João"],
    "Idade": [28, 30],
    "Cidade": ["SP", "RJ"]
}
# Isso vira uma tabela:
#    Nome  Idade Cidade
# 0 Maria     28     SP
# 1  João     30     RJ
```

### **JSON (JavaScript Object Notation)**
O formato JSON (usado em APIs) é praticamente idêntico a um dicionário Python.

```python
import json

# Dicionário para JSON
dados_json = json.dumps(pessoa)

# JSON para Dicionário
dados_dict = json.loads(dados_json)
```

---

## 🔗 Recursos Recomendados

- [Documentação Python - Dicionários](https://docs.python.org/pt-br/3/tutorial/datastructures.html#dictionaries)

---

[⬅️ Voltar ao Índice do Módulo](README.md)