<h1 align="center">Kali Linux & Medusa</h1>
<p align="center"><strong>Desafio prático de segurança ofensiva — DIO</strong></p>
<p align="center">FTP · HTTP / DVWA · SMB / Samba</p>

---

## Sobre o projeto

Este repositório documenta minha experiência prática com auditoria de autenticação e análise de serviços em um laboratório virtual. O objetivo é identificar configurações inseguras, validar resultados e registrar evidências técnicas.

## Ambiente de laboratório

| Componente | Configuração |
| :--- | :--- |
| Máquina de auditoria | Kali Linux |
| Máquina de treinamento | Metasploitable 2 |
| Virtualização | Oracle VirtualBox |
| IP do laboratório | `192.168.56.106` |
| Ferramentas | Nmap, Medusa, Enum4linux, SMBClient, curl e DevTools |

## Resumo dos resultados

| Fase | Serviço | Resultado |
| :--- | :--- | :--- |
| 01 | FTP — porta 21 | Autenticação validada |
| 02 | HTTP / DVWA — porta 80 | Login manual validado; automação inconclusiva |
| 03 | SMB — portas 139 e 445 | Autenticação validada |

## Fase 01 — FTP

Reconhecimento do serviço FTP e validação da autenticação com uma credencial padrão do laboratório.

**Resultado:** Autenticação confirmada pelo Medusa e conexão FTP registrada.

<details>
<summary>Visualizar evidências da fase 01</summary>

### Teste de conectividade

<img src="images/fase1-ftp/01-ping-kali-metasploitable.jpg" alt="Teste de conectividade" width="760">

### IP do laboratório

<img src="images/fase1-ftp/02-ip-metasploitable.jpg" alt="IP do laboratório" width="760">

### Serviços identificados

<img src="images/fase1-ftp/03-nmap-servicos.jpg" alt="Serviços identificados" width="760">

### Resultado do teste FTP

<img src="images/fase1-ftp/04-medusa-ftp-sucesso.jpg" alt="Resultado do teste FTP" width="760">

### Validação da conexão FTP

<img src="images/fase1-ftp/05-conexao-ftp.jpg" alt="Validação da conexão FTP" width="760">

</details>

---

## Fase 02 — HTTP / DVWA

Inspeção do formulário de login, cookies e respostas HTTP.

**Resultado:** Login manual confirmado. O teste automatizado com Medusa apresentou falsos positivos e não foi validado.

<details>
<summary>Visualizar evidências da fase 02</summary>

### Página de login

<img src="images/fase2-dvwa/01-pagina-login.png" alt="Página de login" width="760">

### Inspeção de cookies

<img src="images/fase2-dvwa/02-inspecao-cookies.png" alt="Inspeção de cookies" width="760">

### Redirecionamento HTTP 302

<img src="images/fase2-dvwa/03-redirecionamento-302.png" alt="Redirecionamento HTTP 302" width="760">

### Inspeção do formulário

<img src="images/fase2-dvwa/04-formulario-requisicao.png" alt="Inspeção do formulário" width="760">

### Avisos da ferramenta

<img src="images/fase2-dvwa/05-medusa-avisos.png" alt="Avisos da ferramenta" width="760">

### Falsos positivos

<img src="images/fase2-dvwa/06-medusa-falsos-positivos.png" alt="Falsos positivos" width="760">

### Teste HTTP

<img src="images/fase2-dvwa/07-medusa-teste-http.png" alt="Teste HTTP" width="760">

### Login confirmado

<img src="images/fase2-dvwa/08-login-confirmado.png" alt="Login confirmado" width="760">

</details>

---

## Fase 03 — SMB / Samba

Enumeração de contas, grupos e compartilhamentos com Enum4linux, seguida de auditoria de autenticação e validação pelo SMBClient.

**Resultado:** Autenticação confirmada. Foram listados seis compartilhamentos; acesso root e permissões de escrita não foram comprovados.

O servidor identificou o grupo `WORKGROUP` e os compartilhamentos `print$`, `tmp`, `opt`, `IPC$`, `ADMIN$` e `msfadmin`. Foi observada uma reconexão SMB1.

<details>
<summary>Visualizar evidências da fase 03</summary>

### Enumeração SMB

<img src="images/fase3-smb/01-enum4linux-comando.png" alt="Enumeração SMB" width="760">

### Resultado da enumeração

<img src="images/fase3-smb/02-enum4linux-resultado.png" alt="Resultado da enumeração" width="760">

### Contas e grupos

<img src="images/fase3-smb/03-enumeracao-contas.png" alt="Contas e grupos" width="760">

### Referência da aula (outro IP)

<img src="images/fase3-smb/04-referencia-aula.png" alt="Referência da aula (outro IP)" width="760">

### Listas de treinamento

<img src="images/fase3-smb/05-listas-laboratorio.png" alt="Listas de treinamento" width="760">

### Resultado da auditoria SMB

<img src="images/fase3-smb/06-medusa-resultado.png" alt="Resultado da auditoria SMB" width="760">

### Validação com SMBClient

<img src="images/fase3-smb/07-smbclient-validacao.png" alt="Validação com SMBClient" width="760">

</details>

---

## Aprendizados

- Identificar serviços e verificar a conectividade antes de realizar testes.
- Confirmar resultados com ferramentas independentes.
- Diferenciar redirecionamentos HTTP e falsos positivos de uma autenticação bem-sucedida.
- Reconhecer os riscos de credenciais padrão, protocolos antigos e compartilhamentos expostos.

## Recomendações de segurança

Substituir credenciais padrão, atualizar os serviços, desativar SMB1 quando possível, restringir compartilhamentos e sessões anônimas, limitar tentativas de login e monitorar eventos de autenticação.

## Contexto educacional

Projeto desenvolvido em máquinas virtuais de treinamento. As capturas documentam o laboratório; a referência da aula está identificada separadamente. Não publicar credenciais reais.
