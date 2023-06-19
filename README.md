- 👋 Hi, I’m @Zanchett1
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Zanchett1/Zanchett1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

import random

def gera_numeros_cartao(quantidade, bin_numerico, mes_validade, ano_validade):
    numeros_cartao = []

    for _ in range(quantidade):
        numero = str(bin_numerico) + ''.join(str(random.randint(0, 9)) for _ in range(16 - len(str(bin_numerico))))
        cvv = str(random.randint(100, 999))
        numero += f"/{mes_validade:02d}/{ano_validade:02d}/{cvv}"
        numeros_cartao.append(numero)

    return numeros_cartao

def validar_luhn(numero_cartao):
    # Remove qualquer caractere não numérico
    numero_cartao = ''.join(filter(str.isdigit, numero_cartao))

    # Inverte o número do cartão
    numero_cartao_reverso = numero_cartao[::-1]

    # Calcula a soma dos dígitos, dobrando os dígitos nas posições pares
    soma = sum(int(digito) if indice % 2 == 0 else sum(divmod(int(digito) * 2, 10)) for indice, digito in enumerate(numero_cartao_reverso))

    # O número do cartão é válido se a soma for divisível por 10
    return soma % 10 == 0

quantidade_numeros = int(input("Digite a quantidade de números de cartão a serem gerados: "))
bin_numerico = int(input("Digite o BIN numérico desejado (6 dígitos): "))
mes_validade = int(input("Digite o mês de validade (2 dígitos): "))
ano_validade = int(input("Digite o ano de validade (2 dígitos): "))

numeros_gerados = gera_numeros_cartao(quantidade_numeros, bin_numerico, mes_validade, ano_validade)

contador_validos = 0
contador_invalidos = 0

print("Números de cartão gerados:")
for numero in numeros_gerados:
    valido = validar_luhn(numero)
    print(numero, "- Válido" if valido else "- Inválido")
    
    if valido:
        contador_validos += 1
    else:
        contador_invalidos += 1

print("Total de cartões válidos:", contador_validos)
print("Total de cartões inválidos:", contador_invalidos)

