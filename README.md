# Atendente de IA ao vivo · site que vira contato no WhatsApp

`NO AR` · **Estudo de caso.** O front-end está no repositório do site; o servidor e os prompts são proprietários.

> *EN: Landing page where visitors type their business name and instantly chat, inside a realistic WhatsApp mock-up, with an AI receptionist built for that business. Leads go straight to WhatsApp.*

![Site com o teste ao vivo da atendente](assets/site.png)

**🔗 No ar:** [leomagalhaesti.github.io](https://leomagalhaesti.github.io) · front-end em [leomagalhaesti.github.io](https://github.com/leomagalhaesti/leomagalhaesti.github.io)

---

## O problema

O cliente de um pequeno negócio não entende "atendente com IA" lendo um texto. Ele precisa **ver funcionando com o negócio dele**. Formulário de contato tradicional quase não converte.

## A solução

- O visitante digita o **nome do negócio** e escolhe o ramo (salão, clínica, restaurante, loja, escritório)
- Na hora, um **celular com o WhatsApp** aparece com o nome dele, o ícone do ramo e uma atendente de IA que responde como se trabalhasse lá
- Ele conversa como se fosse o cliente. Quando gosta, pede a **demonstração grátis em 24 h** com nome e WhatsApp
- O pedido chega no meu WhatsApp com a conversa e um botão para montar a demo

```mermaid
flowchart LR
    V[Visitante] -->|nome + ramo| S[Site estático<br/>GitHub Pages]
    S -->|POST /demo| API[Servidor Python<br/>na VPS]
    API --> IA[LLM com persona<br/>do negócio]
    IA --> API --> S
    S -->|pedido de demo| API -->|aviso + conversa| W[WhatsApp do Leo]
```

## Decisões técnicas

| Desafio | Como resolvi |
|---|---|
| Parecer um chat genérico | Celular realista (barra de status com hora real, "Conta comercial", modo escuro) montado em HTML e CSS |
| Abuso e custo de IA | Limite de mensagens por IP por hora no servidor |
| IA falar preço cedo demais | Trava no servidor: se ninguém perguntou preço e a resposta tem "R$", ela é refeita sem valor |
| IA cair | O site mostra o formulário já preenchido com o que a pessoa escreveu |
| Requisição cross-origin | JSON enviado como `text/plain` (sem preflight CORS) |
| Medir o que funciona | Conversas e pedidos registrados por dia. A versão anterior foi trocada porque os dados mostraram 0 pedidos em 20 conversas |

## Stack

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-4285F4?style=flat-square&logo=googlegemini&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=flat-square&logo=githubpages&logoColor=white)

---

Projeto de [Leonardo Magalhães](https://github.com/leomagalhaesti)
