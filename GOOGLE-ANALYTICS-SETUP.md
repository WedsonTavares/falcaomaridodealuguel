# 📊 Guia Completo: Google Analytics 4 & Conversões

## 🎯 Configuração do Google Analytics 4 (GA4)

### Passo 1: Criar Conta no Google Analytics
1. Acesse [Google Analytics](https://analytics.google.com/)
2. Clique em "Começar a medir"
3. Configure:
   - **Nome da conta**: Falcão Marido de Aluguel
   - **Nome da propriedade**: Site Falcão
   - **Fuso horário**: (GMT-03:00) Brasília
   - **Moeda**: Real brasileiro (R$)

### Passo 2: Configurar Fluxo de Dados
1. Escolha **"Web"** como plataforma
2. Insira:
   - **URL do site**: https://falcaomaridodealuguel.com.br
   - **Nome do fluxo**: Site Principal
3. Copie o **ID de medição** (formato: G-XXXXXXXXXX)

### Passo 3: Instalar Código no Site
No arquivo `index.html`, **descomente** estas linhas e substitua `G-XXXXXXXXXX`:

```html
<!-- Google Analytics 4 (Substitua G-XXXXXXXXXX pelo seu ID real) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX', {
    'send_page_view': true,
    'cookie_flags': 'SameSite=None;Secure'
  });
</script>
```

---

## 🏷️ Configuração do Google Tag Manager (GTM)

### Passo 1: Criar Conta no GTM
1. Acesse [Google Tag Manager](https://tagmanager.google.com/)
2. Crie nova conta:
   - **Nome da conta**: Falcão Marido de Aluguel
   - **País**: Brasil
3. Configure container:
   - **Nome do contêiner**: falcaomaridodealuguel.com.br
   - **Plataforma**: Web

### Passo 2: Copiar IDs
Após criar, você receberá:
- **ID do GTM**: GTM-XXXXXXX

### Passo 3: Instalar no Site
No arquivo `index.html`, **descomente** e substitua `GTM-XXXXXXX`:

**No `<head>`:**
```html
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
```

**No `<body>` (logo após a tag de abertura):**
```html
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
```

---

## 🎯 Configuração de Conversões no Google Ads

### Passo 1: Criar Ação de Conversão
1. Acesse [Google Ads](https://ads.google.com/)
2. Vá em **Ferramentas e Configurações** > **Conversões**
3. Clique em **+ Nova ação de conversão**
4. Escolha **Site**
5. Configure:
   - **Categoria**: Lead
   - **Nome**: Clique WhatsApp
   - **Valor**: Use valores diferentes para cada conversão
   - **Contagem**: Uma por clique

### Passo 2: Copiar ID de Conversão
Após criar, você receberá:
- **ID de conversão**: AW-XXXXXXXXXX
- **Rótulo de conversão**: YYYYYYYYYYY

### Passo 3: Substituir no Código
No `index.html`, nos botões WhatsApp, substitua:
```javascript
'send_to': 'AW-CONVERSION_ID/CONVERSION_LABEL'
```

Por:
```javascript
'send_to': 'AW-XXXXXXXXXX/YYYYYYYYYYY'
```

---

## 📈 Eventos Implementados no Site

### 1. **Clique no Header** (whatsapp_header)
```javascript
gtag('event', 'click', {
  'event_category': 'whatsapp',
  'event_label': 'header',
  'value': 1
});
```

### 2. **Clique no Hero** (whatsapp_hero)
```javascript
gtag('event', 'conversion', {
  'event_category': 'whatsapp',
  'event_label': 'hero',
  'value': 1,
  'send_to': 'AW-CONVERSION_ID/CONVERSION_LABEL'
});
```

### 3. **Clique no Contato** (whatsapp_contact)
```javascript
gtag('event', 'conversion', {
  'event_category': 'whatsapp',
  'event_label': 'contact',
  'value': 1,
  'send_to': 'AW-CONVERSION_ID/CONVERSION_LABEL'
});
```

---

## 🔍 Verificar se está Funcionando

### Google Analytics
1. Acesse Google Analytics
2. Vá em **Relatórios** > **Tempo real**
3. Abra seu site em outra aba
4. Você deve ver 1 usuário ativo

### Google Tag Manager
1. Acesse GTM
2. Clique em **Preview**
3. Digite a URL do seu site
4. Navegue pelo site e veja as tags disparando

### Google Ads
1. Acesse Google Ads > Conversões
2. Veja se as conversões aparecem na coluna "Últimos 7 dias"

---

## 📊 Relatórios Importantes no GA4

### 1. **Aquisição**
- De onde vêm os visitantes (Google, WhatsApp, Direto)

### 2. **Engajamento**
- Páginas mais visitadas
- Tempo médio no site
- Taxa de rejeição

### 3. **Conversões**
- Quantos clicaram no WhatsApp
- Qual botão converte mais (header, hero, contato)

### 4. **Tempo Real**
- Visitantes ativos agora
- Páginas sendo visualizadas

---

## 🎯 Metas e KPIs Recomendados

### KPIs Principais
- **Taxa de Conversão**: meta 5-10%
- **Tempo médio no site**: meta 2+ minutos
- **Taxa de rejeição**: meta abaixo de 60%
- **Cliques no WhatsApp**: meta 20+ por semana

### Metas no GA4
1. **Visualização de Página de Contato**
2. **Scroll 75%** (engajamento)
3. **Clique em WhatsApp** (conversão)
4. **Tempo no site > 2min** (engajamento)

---

## 💡 Dicas Avançadas

### 1. **Público-Alvo Personalizado**
Crie públicos no GA4:
- Visitantes que não converteram (remarketing)
- Visitantes que ficaram >2min (público quente)
- Visitantes de Ribeirão Preto (geolocalização)

### 2. **Funil de Conversão**
1. Página Inicial (Hero)
2. Seção Serviços
3. Seção Contato
4. Clique WhatsApp
5. Conversa WhatsApp (fora do site)

### 3. **Teste A/B**
Use Google Optimize para testar:
- Cores dos botões
- Textos dos CTAs
- Posição dos elementos

---

## 🔐 LGPD e Cookies

### Banner de Cookies (Opcional mas Recomendado)
Adicione um banner informando sobre cookies:

```html
<div id="cookie-banner" style="position:fixed;bottom:0;width:100%;background:#222;color:#fff;padding:1rem;text-align:center;">
  Este site usa cookies para melhorar sua experiência. 
  <button onclick="document.getElementById('cookie-banner').style.display='none'">Aceitar</button>
</div>
```

### Política de Privacidade
Crie uma página `privacidade.html` explicando:
- Quais dados coletamos (Analytics, conversões)
- Como usamos (melhorar serviço, anúncios)
- Direitos do usuário (LGPD)

---

## 📞 Suporte

- **Google Analytics**: [Suporte GA4](https://support.google.com/analytics)
- **Google Tag Manager**: [Suporte GTM](https://support.google.com/tagmanager)
- **Google Ads**: [Suporte Ads](https://support.google.com/google-ads)

---

## ✅ Checklist Final

- [ ] Conta GA4 criada
- [ ] ID G-XXXXXXXXXX instalado no site
- [ ] GTM criado e instalado
- [ ] Eventos de conversão configurados
- [ ] Google Ads vinculado ao Analytics
- [ ] Conversões testadas e funcionando
- [ ] Relatórios de tempo real verificados
- [ ] Metas configuradas no GA4
- [ ] Banner de cookies adicionado (opcional)
- [ ] Política de privacidade criada (opcional)

---

**🎉 Com tudo configurado, você terá visibilidade completa sobre:**
- Quantas pessoas visitam o site
- De onde elas vêm
- Quanto tempo ficam
- Quantas clicam no WhatsApp
- Qual horário tem mais conversões
- ROI dos anúncios do Google Ads
