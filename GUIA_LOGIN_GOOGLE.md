# Guia — Ativar login Google no Mapa Eleitoral

Você só precisa fazer **duas coisas**: criar a credencial no Google Cloud e colar no Supabase. Depois me avisa que eu publico o mapa e ligo a segurança.

---

## Dados que você vai usar (copie e cole)

- **URL de callback do Supabase** (o Google precisa dela):
  `https://xofegurmrfkaavhtndqk.supabase.co/auth/v1/callback`
- **Origem do site (GitHub Pages):**
  `https://dimensconsulting.github.io`
- **Endereço do mapa (confirme se é este que você abre):**
  `https://dimensconsulting.github.io/Cezinha-de-Madureira/mapa-demografico-votos.html`

---

## Parte 1 — Google Cloud (criar a credencial OAuth)

1. Acesse **https://console.cloud.google.com** com a conta `dimensconsulting@gmail.com`.
2. No topo, crie/seleciona um projeto (ex.: "Cezinha Mapa").
3. Menu → **APIs e serviços → Tela de permissão OAuth** (OAuth consent screen):
   - Tipo de usuário: **Externo** → Criar.
   - Nome do app: `Mapa Eleitoral Cezinha`; e-mail de suporte: seu e-mail; e-mail do desenvolvedor: seu e-mail. Salvar e continuar até o fim.
   - Em **Usuários de teste**, se o app ficar em modo "Teste", adicione os e-mails que vão logar (ou publique o app depois em "Produção" para liberar geral). *A aprovação de acesso é controlada por nós no painel do mapa, então não precisa restringir aqui.*
4. Menu → **APIs e serviços → Credenciais → Criar credenciais → ID do cliente OAuth**:
   - Tipo de aplicativo: **Aplicativo da Web**.
   - **Origens JavaScript autorizadas** → adicionar: `https://dimensconsulting.github.io`
   - **URIs de redirecionamento autorizados** → adicionar exatamente: `https://xofegurmrfkaavhtndqk.supabase.co/auth/v1/callback`
   - Criar.
5. Copie o **Client ID** e o **Client Secret** que aparecem.

---

## Parte 2 — Supabase (ativar o provedor Google)

1. Acesse **https://supabase.com/dashboard**, projeto **xofegurmrfkaavhtndqk**.
2. Menu **Authentication → Sign In / Providers → Google**:
   - Ative (Enable).
   - Cole o **Client ID** e o **Client Secret** do passo anterior.
   - Salvar.
3. Menu **Authentication → URL Configuration**:
   - **Site URL:** `https://dimensconsulting.github.io/Cezinha-de-Madureira/mapa-demografico-votos.html`
   - **Redirect URLs → Add URL:** `https://dimensconsulting.github.io/Cezinha-de-Madureira/mapa-demografico-votos.html`
   - (Opcional, para testes locais, adicione também a URL que você usa ao abrir o arquivo.)
   - Salvar.

---

## Parte 3 — Me avisa

Quando terminar as Partes 1 e 2, me diga **"Google configurado"**. Aí eu:
1. Publico a versão do mapa com login (git).
2. Ligo a segurança no banco (só quem está aprovado enxerga os dados).

Você entra com `dimensconsulting@gmail.com` e já cai como **admin** automaticamente. Qualquer outra pessoa que entrar fica **pendente**, e você aprova (e define leitura/edição/admin) no botão de **Controle de acesso** no topo do mapa.

---

### Observações
- **Nada de senha é digitado por mim** — a credencial Google fica só com você, no painel.
- O site interno (index.html) **continua funcionando normal**, sem login.
- Enquanto o Google não estiver configurado, **não publico** a versão com login, para o mapa atual não ficar inacessível.
