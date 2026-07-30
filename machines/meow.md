<h1 align="center"> [Nome do Alvo] — Write-up </h1>

<p align="center"><a href="https://app.hackthebox.com/public/users/3757032"><img src="https://custom-icon-badges.demolab.com/badge/HackTheBox-111927?style=for-the-badge&logo=hackthebox&logoColor=9FEAF9" alt="HackTheBox" /></a>&nbsp;<a href="https://tryhackme.com/p/iswia"><img src="https://custom-icon-badges.demolab.com/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=red" alt="TryHackMe" /></a></p>

</br>

## Informações Gerais

| Campo | Detalhe |
|---|---|
| Plataforma | HackTheBox / TryHackMe / Outro |
| Dificuldade | Fácil / Médio / Difícil / Insano |
| Sistema Operacional | Linux / Windows |
| IP do alvo | 10.10.10.x |
| Data | DD/MM/AAAA |
| Técnicas envolvidas | ex: SQLi, SUID abuse, Kerberoasting |

</br>

## Resumo Executivo

> Breve parágrafo (3-5 linhas) resumindo o vetor de ataque principal e o resultado final (ex: acesso root/SYSTEM obtido via X, explorando Y). Escreva como se fosse ler antes de qualquer outra seção — é o que um recrutador ou cliente lê primeiro.

</br>

## 1. Reconhecimento

### 1.1 Varredura de portas

```bash
nmap -sC -sV -oN nmap/initial.txt 10.10.10.x
```

**Resultado:**
```
[cole o output relevante aqui]
```

**Análise:** quais portas/serviços chamaram atenção e por quê.

### 1.2 Varredura completa (opcional)

```bash
nmap -p- -oN nmap/full.txt 10.10.10.x
```

</br>

## 2. Enumeração

Para cada serviço relevante, documente o raciocínio — não só o comando.

### 2.1 [Serviço, ex: HTTP - porta 80]

- Ferramentas usadas: `gobuster`, `whatweb`, navegação manual, etc.
- O que foi encontrado (diretórios, versões, tecnologias)
- Por que isso foi investigado (hipótese que estava testando)

```bash
gobuster dir -u http://10.10.10.x -w /path/to/wordlist -o gobuster.txt
```

### 2.2 [Outro serviço, ex: SMB - porta 445]

```bash
smbclient -L //10.10.10.x -N
```

Resultado e análise.

</br>

## 3. Exploração

### 3.1 Vulnerabilidade identificada

Descreva a falha (ex: RCE em versão desatualizada de X, LFI, credenciais fracas).

### 3.2 Prova de conceito / Exploração

```bash
[comando ou payload usado]
```

**Explicação:** por que esse payload/exploit funciona (mecanismo da vulnerabilidade, não só "rodei e funcionou").

### 3.3 Acesso obtido

```
[shell obtido, output do whoami, id, etc.]
```

</br>

## 4. Escalação de Privilégio

### 4.1 Enumeração local

```bash
[linpeas.sh / winpeas.exe / comandos manuais]
```

**Vetor encontrado:** (ex: SUID binary mal configurado, serviço rodando como root, senha reutilizada em outro arquivo)

### 4.2 Exploração do vetor

```bash
[comando de exploração]
```

### 4.3 Acesso privilegiado confirmado

```
[output de whoami / id mostrando root ou SYSTEM]
```

</br>

## 5. Flags

> ⚠️ Nunca publique a flag real — use placeholder ou hash parcial.

| Flag | Localização |
|---|---|
| user.txt | `/home/user/user.txt` |
| root.txt | `/root/root.txt` |

</br>

## 6. Lições Aprendidas

- O que travou você durante a resolução e como destravou
- O que você faria diferente numa próxima vez
- Conceitos novos aprendidos (técnica, ferramenta, tipo de vulnerabilidade)
- Como essa vulnerabilidade se conecta a cenários reais (ex: "esse tipo de má configuração é comum em ambientes corporativos que...")

</br>

## 7. Mitigação

> Seção que simula a entrega real de um relatório de pentest profissional — mostra que você pensa além de "consegui invadir".

| Vulnerabilidade | Risco | Recomendação |
|---|---|---|
| ex: Samba desatualizado | Alto | Atualizar para versão X, aplicar patch Y |
| ex: SUID mal configurado | Médio | Remover bit SUID de binários não essenciais |

</br>

## Referências

- [Link para CVE, se aplicável]
- [Link para documentação da ferramenta usada]
- [Link para write-ups ou artigos que ajudaram, se usados]
