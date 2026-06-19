# Dívida Zero — Deploy no Vercel

## Estrutura do projeto

```
divida-zero/
├── api/
│   ├── criar-pix.js      ← Gera transação Pix via MisticPay
│   └── verificar-pix.js  ← Verifica status do pagamento
├── public/
│   └── index.html        ← Landing page com 3 planos
├── package.json
├── vercel.json
└── README.md
```

## Como publicar no Vercel (passo a passo)

### 1. Instale o Vercel CLI (opcional)
```bash
npm install -g vercel
```

### 2. Faça upload do projeto
- Acesse https://vercel.com
- Clique em "Add New Project"
- Arraste a pasta `divida-zero` ou conecte ao GitHub

### 3. Configure as variáveis de ambiente (IMPORTANTE)
No painel do Vercel, vá em Settings → Environment Variables e adicione:

| Variável | Valor |
|---|---|
| MISTICPAY_CI | ci_1a3q6njdt57xurt |
| MISTICPAY_CS | cs_rhcv5wstvu2hxsf9q0bnvg3xk |

### 4. Deploy
Clique em "Deploy". Pronto — seu site estará no ar em minutos.

## Como funciona o checkout

1. Cliente escolhe um plano e clica no botão
2. Modal abre pedindo nome e CPF
3. Backend chama a API MisticPay e gera o QR Code Pix
4. Cliente escaneia ou copia o código e paga
5. A cada 5 segundos o site verifica o status automaticamente
6. Quando confirmado, exibe a tela de sucesso

## Planos configurados

| Plano | ID | Valor |
|---|---|---|
| Essencial | essencial | R$25,90 |
| Completo | completo | R$47,90 |
| Master | master | R$89,90 |

Para alterar valores, edite o objeto `PLANOS` em `api/criar-pix.js`.

## Personalizar entrega do produto

Após confirmar o pagamento, você precisa entregar o material ao cliente.
Opções recomendadas:
- Webhook da MisticPay → enviar e-mail automático com link
- Ou monitorar o painel da MisticPay e enviar manualmente

## Suporte MisticPay
- Docs: https://docs.misticpay.com
- Email: contato@misticpay.com
