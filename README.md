# 🔐 Lab de Segurança: Ataques de Força Bruta com Kali Linux + Medusa

## 📌 Objetivo

Este projeto tem como objetivo simular ataques de força bruta em um ambiente controlado, utilizando ferramentas de segurança ofensiva, com foco em autenticação web vulnerável.

O trabalho também incorpora um estudo de caso real, conectando teoria e prática para demonstrar entendimento completo do cenário de segurança.

---

## 🧱 Ambiente Utilizado

* Kali Linux (máquina atacante)
* DVWA (Damn Vulnerable Web Application) rodando em ambiente local (Laragon)
* VirtualBox 
* Ferramentas:

  * Medusa
  * Hydra

---

## 🌐 Arquitetura do Ambiente

```text
[Kali Linux VM]  --->  [Windows 10 VM - DVWA]
        |                       |
     (Ataque)              (Alvo vulnerável)
```

* Kali: `123.456.78.910`
* DVWA: `123.132.12.1`

---

## 🔎 Enumeração Inicial

Validação de conectividade:

```bash
ping 123.132.12.1
```

Acesso à aplicação:

```
http://123.132.12.1/DVWA
```

---

## ⚔️ Ataque de Força Bruta

### 📄 Wordlist utilizada

Arquivo: `wordlist.txt`

```
admin
password
123456
root
test
```

---

## 🧪 Teste com Medusa

```bash
medusa -h 123.132.12.1 \
-u admin \
-P wordlist.txt \
-M http \
-m FORM:"/DVWA/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed"
```

### ⚠️ Observação

O Medusa apresentou limitações ao lidar com formulários HTTP baseados em sessão, resultando em possíveis falsos positivos.

---

## 🧪 Teste com Hydra

```bash
hydra -l admin -P wordlist.txt 123.132.12.1 http-post-form \
"/projetos-pessoais/DVWA/login.php:username=^USER^&password=^PASS^&Login=Login:F=Login failed"
```

### ⚠️ Desafios encontrados

* Falsos positivos devido à validação incorreta da resposta HTTP
* Dificuldade em diferenciar sucesso e falha em aplicações com sessão
* Sensibilidade da ferramenta à sintaxe e parâmetros

---

## ✅ Validação Manual

Credencial válida confirmada:

* Usuário: `admin`
* Senha: `password`

A validação manual foi necessária devido às limitações das ferramentas automatizadas.

---

## 🧠 Aprendizados

Durante o projeto, foram identificados pontos importantes:

* Ferramentas de brute force não são infalíveis
* Aplicações web modernas exigem controle de sessão
* Falsos positivos são comuns em testes automatizados
* Validação manual é essencial em segurança ofensiva

---

## 🔎 Estudo de Caso Real

Foi realizado previamente um relatório de vulnerabilidades em um ambiente real, onde foram identificadas falhas como:

* Endpoint de autenticação sem rate limiting
* Possibilidade de brute force
* Exposição de serviços sensíveis

Este laboratório foi utilizado para simular, em ambiente controlado, o impacto dessas vulnerabilidades.

---

## 🛡️ Recomendações de Segurança

* Implementar rate limiting em autenticação
* Bloquear após múltiplas tentativas
* Utilizar autenticação multifator (MFA)
* Monitorar logs de acesso
* Utilizar HTTPS

---

## ⚠️ Considerações Éticas

Este projeto foi realizado exclusivamente em ambiente controlado para fins educacionais.

Nenhum sistema real foi atacado ou explorado sem autorização.

---

## 📂 Estrutura do Repositório

```
kali-medusa-lab/
│
├── README.md
├── wordlist.txt
├── images/
│   └── (prints dos testes)
```

---

## 📸 Evidências (Opcional)

Adicione prints de:

* DVWA acessível pelo Kali
* execução do Medusa
* execução do Hydra
* tentativa de login

---

## 🚀 Conclusão

Este projeto demonstra na prática como ataques de força bruta funcionam, suas limitações e a importância de validação correta dos resultados.

Além disso, evidencia a necessidade de boas práticas de segurança em sistemas web.

---
