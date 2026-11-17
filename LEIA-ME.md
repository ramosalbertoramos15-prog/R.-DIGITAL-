# R DIGITAL — como pôr o site online (grátis)

Ficheiros: `index.html` (o site), `supabase.sql` (base de dados), `vercel.json` (segurança).

## 1. Base de dados (Supabase)
1. Crie conta em supabase.com e um projeto novo.
2. SQL Editor > New query > cole o conteúdo de `supabase.sql` > Run.
3. Settings > API: copie o **Project URL** e a chave **anon public**.
4. Cole os dois em `index.html`, na secção `CONFIG` (SUPABASE_URL e SUPABASE_ANON_KEY).
5. Na mesma secção preencha **PAYMENTS** com o nome e número das suas contas M-Pesa, e-Mola e BIM (conta e NIB).

## 2. Login com Google e Facebook
Supabase > Authentication > Providers: ative Google e Facebook e cole as chaves
(Google Cloud Console e Meta for Developers). Em Authentication > URL Configuration,
ponha o endereço do seu site em **Site URL**. Email e palavra-passe já funcionam.

## 3. GitHub
1. Crie um repositório novo no GitHub (por exemplo `rdigital`).
2. Envie os 3 ficheiros (Add file > Upload files) e faça Commit.

## 4. Online (Vercel)
1. vercel.com > Add New > Project > escolha o repositório > Deploy.
2. Em poucos segundos recebe o endereço público. Depois compre um domínio (.co.mz ou .com) e ligue em Settings > Domains.

## 5. Tornar-se administrador
Crie a sua conta no site. Depois, no Supabase SQL Editor, execute (com o seu email):

    update public.profiles set is_admin = true where email = 'SEU_EMAIL';

Entre de novo no site: aparece o botão **Painel**. Lá vê pedidos, comprovativos,
clientes (quem entrou e quem nunca entrou) e edita preços. Só você vê isto.

## 6. Free Fire
Painel > Produtos: ponha o preço de "Recarga Free Fire" e marque **Visível**. Para vários pacotes, use "Novo produto" (marque "Pede ID do jogador").

## Segurança já incluída
- Regras RLS: cada cliente só vê os seus pedidos; só administradores veem todos.
- Preço e estado do pedido são decididos no servidor, o cliente não os altera.
- Comprovativos em pasta privada (links temporários de 5 minutos).
- Cabeçalhos HTTPS/CSP no `vercel.json`. Nunca se guardam dados de cartão.
- Contra quedas: Vercel usa rede global (CDN). Ative a verificação de email e CAPTCHA em Supabase > Authentication.
- Não partilhe a chave `service_role` do Supabase. A chave `anon` é pública por desenho.
