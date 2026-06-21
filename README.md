# Sítio Vô Procópio — site & configuração de domínio

Site institucional do **Sítio Vô Procópio** e documentação de toda a
configuração do domínio `sitiovoprocopio.com.br`.

Este repositório serve hoje as páginas via **GitHub Pages**. As páginas de
**Termos de Uso** e **Política de Privacidade** são obrigatórias para a
aprovação (Production review) da API de publicação do **TikTok** da conta
[@sitiovoprocopio](https://www.tiktok.com/@sitiovoprocopio).

> ⚠️ **Se for trocar a hospedagem** (ex.: site novo feito por terceiros/cowork),
> leia a seção [Migração para um site novo](#migração-para-um-site-novo) antes —
> há itens que **precisam ser preservados** para não quebrar e-mail e TikTok.

---

## Estrutura do repositório

```
.
├── index.html              # landing page
├── style.css               # estilos compartilhados
├── termos/index.html       # Termos de Uso        → /termos/
├── privacidade/index.html  # Política de Privacidade → /privacidade/
└── CNAME                   # domínio custom do GitHub Pages
```

URLs públicas (após DNS no ar):
- `https://sitiovoprocopio.com.br/`
- `https://sitiovoprocopio.com.br/termos/`
- `https://sitiovoprocopio.com.br/privacidade/`

---

## Domínio

| Item | Valor |
|------|-------|
| Domínio | `sitiovoprocopio.com.br` |
| Registrador | **registro.br** |
| DNS | Servidores DNS do próprio registro.br (zona editada no painel) |

---

## DNS — registros configurados no registro.br

Painel: **registro.br → Meus domínios → sitiovoprocopio.com.br → DNS →
Configurar endereçamento → Modo avançado** (editor de zona).

Em **todas** as entradas o campo **Nome fica vazio** (raiz do domínio — o
registro.br não aceita `@`).

| Tipo | Nome | Dados | Para quê |
|------|------|-------|----------|
| A | *(vazio)* | `185.199.108.153` | GitHub Pages (site) |
| A | *(vazio)* | `185.199.109.153` | GitHub Pages (site) |
| A | *(vazio)* | `185.199.110.153` | GitHub Pages (site) |
| A | *(vazio)* | `185.199.111.153` | GitHub Pages (site) |
| MX | *(vazio)* | `10 mx1.improvmx.com` | E-mail (encaminhamento) |
| MX | *(vazio)* | `20 mx2.improvmx.com` | E-mail (encaminhamento) |
| TXT | *(vazio)* | `v=spf1 include:spf.improvmx.com ~all` | SPF (anti-spam do e-mail) |

> Domínio `.com.br` recém-registrado fica **"em transição"** por algumas horas;
> o editor de zona só aceita salvar depois que a transição termina.

---

## Hospedagem — GitHub Pages

| Item | Valor |
|------|-------|
| Repositório | `github.com/procsrib/sitiovoprocopio-site` (público) |
| Branch publicada | `master` (raiz `/`) |
| Domínio custom | definido pelo arquivo `CNAME` (`sitiovoprocopio.com.br`) |
| HTTPS | Certificado Let's Encrypt automático do GitHub (após o DNS apontar) |

**Como editar/publicar:** qualquer commit na branch `master` republica o site
automaticamente em ~1 min. URLs com pasta (`/termos/`) vêm de
`termos/index.html`.

**Habilitar HTTPS:** depois que os registros A propagarem, em
*Settings → Pages* do repositório, marque **"Enforce HTTPS"**.

---

## E-mail — encaminhamento via ImprovMX

Endereço institucional **`contato@sitiovoprocopio.com.br`** (usado nas páginas
legais) é encaminhado para o e-mail pessoal do proprietário através do serviço
gratuito **[ImprovMX](https://improvmx.com)**.

- Configuração do alias (`contato` → e-mail de destino) fica no **painel do
  ImprovMX**, não neste repositório.
- Os registros **MX** + **TXT (SPF)** acima são o que faz o encaminhamento
  funcionar.

---

## Integração com redes sociais (contexto)

O conteúdo do sítio é publicado automaticamente nas redes pela automação do
agente `conexao-sitio` (infraestrutura separada, repositório privado):

- **Instagram** `@sitiovoprocopio` — Meta Graph API ✅ em produção
- **Facebook** Page *Sítio Vô Procópio* — espelho automático do IG ✅
- **TikTok** `@sitiovoprocopio` — código pronto; **aguardando Production review**
  do TikTok, que exige as URLs públicas de Termos e Privacidade deste site.

> Nenhuma credencial/token fica neste repositório — apenas o site estático.

---

## Migração para um site novo

Se o site for refeito em outra plataforma/ferramenta, **preserve**:

1. **As URLs de Termos e Privacidade** — `https://sitiovoprocopio.com.br/termos/`
   e `/privacidade/` precisam continuar acessíveis (estão registradas no TikTok
   Developer Portal). Se mudarem de caminho, atualizar lá também.
2. **Os registros de e-mail** (MX + TXT do ImprovMX) — não remover, senão o
   `contato@sitiovoprocopio.com.br` para de funcionar.
3. **HTTPS** — o TikTok exige as páginas legais com `https://`.

O que **muda** ao trocar de hospedagem:
- Os **4 registros A** acima são específicos do GitHub Pages. Uma nova
  hospedagem dará outro IP/endereço — substituir os A (ou usar CNAME, conforme
  a plataforma) e ajustar/retirar o `CNAME` deste repositório.

---

*Última atualização desta documentação: 2026-06-21.*
