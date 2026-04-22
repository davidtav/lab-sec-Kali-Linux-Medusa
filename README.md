# 🔐 Lab de Segurança: Ataques de Força Bruta com Kali Linux + Medusa

## 📌 Objetivo

Este projeto tem como objetivo simular ataques de força bruta em um ambiente controlado, utilizando ferramentas de segurança ofensiva, com foco em autenticação web vulnerável.

O trabalho também incorpora um estudo de caso real, conectando teoria e prática para demonstrar entendimento completo do cenário de segurança.

---

## 🧱 Ambiente Utilizado

* Kali Linux (máquina atacante)
* DVWA (Damn Vulnerable Web Application) rodando em VM
* VirtualBox
* Ferramentas:

  * Medusa
  * Hydra

---

## 🌐 Arquitetura do Ambiente

```
[Kali Linux VM]  --->  [Windows10 VM - DVWA]
        |                       |
     (Ataque)              (Alvo vulnerável)
```

* Kali: `192.16x.xx.xxx`
* DVWA: `192.16x.xx.xxx`

---

## 🔎 Enumeração Inicial

Validação de conectividade:

```bash
ping 192.16x.xx.xxx
```

Acesso à aplicação:

```
http://192.16x.xx.xxx/DVWA
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
medusa -h 192.16x.xx.xxx \
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
hydra -l admin -P wordlist.txt 192.16x.xx.xxx http-post-form \
"/DVWA/login.php:username=^USER^&password=^PASS^&Login=Login:F=Login failed"
```

---

## ⚠️ Limitações das Ferramentas

Durante os testes, foram observadas limitações importantes nas ferramentas utilizadas:

* O Medusa não possui suporte completo para formulários HTTP com autenticação baseada em sessão
* O Hydra exige configuração precisa da validação de resposta, podendo gerar falsos positivos
* A detecção de sucesso/falha em aplicações web depende da análise correta de redirecionamentos e conteúdo HTML

Esses desafios refletem cenários reais de testes de segurança, onde ajustes manuais e validação humana são essenciais.

---

## 🧪 Boas Práticas Aplicadas

* Execução apenas em ambiente controlado
* Não realização de ataques em sistemas reais sem autorização
* Sanitização de dados sensíveis (IPs e caminhos)
* Validação manual dos resultados obtidos

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
* A configuração incorreta de parâmetros pode comprometer os resultados

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
* Evitar mensagens detalhadas de erro em autenticação

---

## ⚠️ Considerações Éticas

Este projeto foi realizado exclusivamente em ambiente controlado para fins educacionais.

Nenhum sistema real foi atacado ou explorado sem autorização.

---

## 📂 Estrutura do Repositório

```
lab-sec-Kali-Linux-Medusa/
│
├── README.md
├── wordlist.txt
├── images/
│   └── (prints dos testes)
```

---

## 📸 Evidências

Sugestões de capturas de tela:

* DVWA acessível via Kali Linux
* Execução dos comandos Medusa e Hydra
* Tentativas de autenticação
* Validação manual do login

---

## 🚀 Conclusão

Este projeto demonstra na prática como ataques de força bruta funcionam, suas limitações e a importância de validação correta dos resultados.

Além disso, evidencia a necessidade de boas práticas de segurança em sistemas web e o papel crítico da análise manual em testes de segurança.

---

> 🔒 Os endereços IP e caminhos foram parcialmente mascarados para preservar boas práticas de segurança e privacidade.
