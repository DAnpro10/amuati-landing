# Proposta mínima — Landing page da Amua TI

## Objetivo
Criar uma landing page institucional simples, rápida e com foco em conversão, com:
- visual limpo/premium;
- CTA claro para WhatsApp e e-mail;
- formulário enxuto para captura de leads;
- possibilidade de publicar grátis para teste inicial.

## Recomendação prática para o teste inicial
**Melhor opção agora: manter estático e publicar no GitHub Pages ou Vercel.**

Por quê:
- a landing atual é estática e já resolve o teste visual/comercial;
- o custo e a complexidade ficam praticamente zero;
- para validar interesse, geralmente basta CTA para WhatsApp + e-mail + formulário simples;
- backend próprio só vale a pena se houver necessidade real de armazenar leads internamente.

### Quando usar backend
Só vale criar backend se vocês quiserem:
- salvar leads em banco;
- integrar com CRM;
- disparar e-mail automático;
- ter painel interno para acompanhamento.

Para o primeiro teste, eu recomendo **não criar backend próprio**. Se precisar captar leads, usar um serviço simples de formulário, como:
- Formspree;
- Netlify Forms;
- Getform;
- Supabase Functions / DB, se já houver stack com Supabase.

---

## Estrutura mínima de arquivos

### Opção 1 — mais simples, 100% estática
```text
amuati-landing/
├─ index.html
├─ assets/
│  ├─ css/
│  │  └─ main.css
│  ├─ js/
│  │  └─ main.js
│  └─ img/
│     ├─ logo.svg
│     └─ og-image.jpg
└─ README.md
```

### Opção 2 — com captura de leads simples via backend/serverless
```text
amuati-landing/
├─ index.html
├─ assets/
│  ├─ css/main.css
│  ├─ js/main.js
│  └─ img/
├─ api/
│  └─ lead.js           # função serverless opcional
└─ README.md
```

### Se a ideia for evoluir para frontend em componentes
```text
src/
├─ components/
│  ├─ Header.tsx
│  ├─ Hero.tsx
│  ├─ Services.tsx
│  ├─ Process.tsx
│  ├─ Differentials.tsx
│  └─ ContactForm.tsx
├─ data/
│  └─ content.ts
├─ styles/
│  └─ globals.css
└─ pages/
   └─ index.tsx
```

---

## Componentes/seções sugeridas

A landing atual já está bem próxima do que eu faria. A estrutura mínima ideal é:

1. **Header fixo**
   - logo/nome Amua TI;
   - navegação âncora: Serviços, Processo, Diferenciais, Contato;
   - CTA principal: “Solicitar diagnóstico”.

2. **Hero**
   - headline forte;
   - subtítulo explicando valor;
   - 2 CTAs:
     - WhatsApp;
     - formulário/contato.
   - bloco lateral com prova visual/benefícios rápidos.

3. **Serviços**
   - cards curtos:
     - suporte técnico;
     - segurança digital;
     - redes e infraestrutura;
     - nuvem e automação.

4. **Como funciona**
   - fluxo em 4 passos:
     - diagnóstico;
     - plano;
     - implantação;
     - suporte contínuo.

5. **Diferenciais**
   - linguagem curta e comercial;
   - foco em clareza, agilidade e proximidade.

6. **Contato / Formulário**
   - nome;
   - empresa;
   - e-mail;
   - WhatsApp;
   - descrição da necessidade;
   - botão enviar.

7. **Footer**
   - direitos básicos;
   - contatos resumidos;
   - link WhatsApp/e-mail.

---

## Comportamento do formulário

### Versão mínima recomendada
O formulário pode fazer 3 coisas:

1. **Validar campos obrigatórios no front-end**
   - nome;
   - e-mail;
   - WhatsApp;
   - mensagem.

2. **Enviar para um endpoint simples**
   - `POST /api/lead` (se houver backend);
   - ou serviço externo de formulário, se a página continuar estática.

3. **Feedback visual imediato**
   - estado de carregando;
   - sucesso: “Recebemos sua mensagem”;
   - erro: “Não foi possível enviar, tente novamente”.

### UX recomendado
- botão desabilitado enquanto envia;
- máscara básica para telefone, se possível;
- prevenção de spam simples com honeypot oculto;
- fallback de CTA caso o envio falhe: abrir WhatsApp.

### Fluxo sugerido
- usuário preenche;
- front-end faz validação;
- envia JSON para o backend/serviço;
- backend registra lead e responde `200 OK`;
- front-end mostra confirmação.

---

## CTA de WhatsApp e e-mail

### WhatsApp
Usar link direto:
```text
https://wa.me/55DDDNÚMERO?text=Olá%20Amua%20TI,%20quero%20um%20diagnóstico.
```

Exemplo de comportamento:
- no hero: botão primário “Falar no WhatsApp”;
- no topo fixo: CTA persistente;
- no formulário: fallback de contato.

### E-mail
Usar `mailto:` como fallback rápido:
```text
mailto:contato@amuati.com.br?subject=Quero%20um%20diagnóstico
```

Recomendação prática:
- WhatsApp como CTA principal de conversão;
- e-mail como opção secundária e institucional.

---

## Abordagem de backend simples para captura de leads

### Recomendação principal: sem backend próprio no primeiro teste
Se o objetivo é só validar interesse, o melhor custo/benefício é:
- manter estático;
- publicar no GitHub Pages ou Vercel;
- usar Formspree/Netlify Forms para captar leads.

Isso evita:
- deploy de API;
- configuração de banco;
- manutenção extra;
- risco de o backend virar bloqueio para publicar.

### Se quiser backend mínimo mesmo assim
Uma opção leve é criar uma função serverless:

#### Exemplo de arquitetura
- `POST /api/lead`
- validação de payload
- gravação em banco simples ou planilha
- resposta JSON

#### Payload sugerido
```json
{
  "name": "Fulano",
  "company": "Empresa X",
  "email": "fulano@empresa.com",
  "phone": "11999999999",
  "message": "Quero suporte para infraestrutura"
}
```

#### Processamento mínimo
- validar campos obrigatórios;
- normalizar telefone;
- registrar data/hora;
- salvar em banco ou enviar por e-mail.

### Implementação mínima recomendada se houver backend
- **Vercel Functions** se hospedar na Vercel;
- **Netlify Functions** se hospedar na Netlify;
- **Supabase** se quiser persistência simples com tabela `leads`.

### Tabela de leads sugerida
Campos mínimos:
- id
- created_at
- name
- company
- email
- phone
- message
- source
- status

---

## Ajustes que eu faria na página atual

A landing atual já está boa como base. Para versão de teste, eu sugeriria:
- trocar telefones/e-mail placeholders por dados reais;
- deixar o CTA do hero e do header apontando para o mesmo fluxo;
- conectar o formulário a um destino real;
- incluir prova social, se existir:
  - clientes;
  - depoimentos;
  - certificações;
  - áreas atendidas.

---

## Melhor caminho para o link free de teste

### Opção mais simples e prática
1. manter o site estático;
2. subir no **GitHub Pages** ou **Vercel**;
3. apontar o formulário para um serviço externo;
4. usar WhatsApp como conversão principal.

### Minha recomendação final
Para o primeiro teste da Amua TI:
- **front-end estático**;
- **sem backend próprio**;
- **WhatsApp + e-mail + formulário com serviço externo**;
- publicar em **Vercel ou GitHub Pages**.

Isso entrega o link free mais rápido e com menos risco.
