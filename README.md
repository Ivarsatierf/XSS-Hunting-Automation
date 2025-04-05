
# 🚀 XSS Hunting Automation – Recon to Exploit

Automação completa para caça de vulnerabilidades **XSS (Cross-Site Scripting)** usando ferramentas poderosas do mundo Bug Bounty. Esse script faz a coleta de URLs, filtra os parâmetros e dispara testes automáticos com payloads customizados via `dalfox`.

> 📌 Ideal para bug hunters, red teamers e estudantes de pentest que querem ganhar tempo e automatizar parte do processo de reconhecimento + exploração.

---

## 📦 Requisitos

Certifique-se de ter as seguintes ferramentas instaladas no seu sistema:

- [`waybackurls`](https://github.com/tomnomnom/waybackurls)
- [`gf`](https://github.com/tomnomnom/gf)
- [`uro`](https://github.com/s0md3v/uro)
- [`Gxss`](https://github.com/KathanP19/Gxss)
- [`kxss`](https://github.com/t3l3machus/kxss)
- [`dalfox`](https://github.com/hahwul/dalfox)
- [`go`](https://go.dev/doc/install)
- [`curl`, `grep`, `sed`, `tee`, `sort`, `cat`]

---

## 🔧 Instalação Rápida

```bash
# Instalar waybackurls, gf, uro, Gxss, kxss e dalfox
go install github.com/tomnomnom/waybackurls@latest
go install github.com/tomnomnom/gf@latest
go install github.com/s0md3v/uro@latest
go install github.com/KathanP19/Gxss@latest
go install github.com/t3l3machus/kxss@latest
go install github.com/hahwul/dalfox/v2@latest

# Adicione as ferramentas ao PATH (Gxss e kxss usam comunicação local, atente-se ao burp/collaborator se necessário)
export PATH=$PATH:$(go env GOPATH)/bin
```
## COMANDOS E EXPLIÇÃO
```bash
COMANDO: echo "http://testphp.vulnweb.com/" | waybackurls | gf xss | uro | Gxss | kxss | tee XSSurls.txt

# Coleta de URLs via Wayback e aplicação de filtros XSS com gf, uro, Gxss e kxss
echo "http://testphp.vulnweb.com/" \
  | waybackurls \
  | gf xss \
  | uro \
  | Gxss \
  | kxss \
  | tee XSSurls.txt

COMANDO: cat XSSurls.txt | grep -oP '^URL: \K\S+' | sed 's/=.*=/=/' | sort -u > final.txt

# Extração de URLs com parâmetros e limpeza
cat XSSurls.txt \
  | grep -oP '^URL: \K\S+' \
  | sed 's/=.*=/=/' \
  | sort -u \
  > final.txt

# Escaneamento com payloads customizados
COMANDO: dalfox file final.txt --custom-payload XSSpayloads.txt --mass
```
