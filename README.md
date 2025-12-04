🛠️ Manual de Configuração: Painel no GitHub com Login Próprio

Este guia explica como configurar o seu próprio banco de dados para que o sistema de Cadastro e Login funcione perfeitamente quando hospedado no GitHub Pages.

🚀 Parte 1: Criar o Banco de Dados (Firebase)

O GitHub é apenas para visualizar o site. Para salvar usuários e senhas, usamos o Google Firebase (gratuito).

Aceda a console.firebase.google.com e faça login com a sua conta Google.

Clique em "Adicionar projeto" (ou "Create a project").

Dê um nome (ex: painel-otica-seunome).

Desative o Google Analytics (não é necessário agora).

Clique em "Criar projeto".

Ativar a Autenticação (Para o sistema funcionar)

No menu lateral esquerdo, clique em Criação (Build) > Authentication.

Clique em "Vamos começar".

Na aba "Sign-in method", selecione Anônimo (Anonymous).

Ative a chave ("Enable") e clique em Salvar.

Nota: O nosso código usa login Anônimo nos bastidores para conectar ao banco, enquanto gere o utilizador/senha que criou na tela de login.

Criar o Banco de Dados (Firestore)

No menu lateral, clique em Criação (Build) > Firestore Database.

Clique em "Criar banco de dados".

Escolha a localização (pode ser nam5 ou us-central).

Importante: Escolha iniciar no modo de teste (Start in test mode) para facilitar a configuração inicial.

Atenção: O modo de teste expira em 30 dias. Para produção, configure as regras de segurança mais tarde.

Clique em Criar.

🔑 Parte 2: Obter a Configuração (As Chaves)

Dentro do seu projeto Firebase, clique na engrenagem ⚙️ (Configurações do projeto) no topo do menu lateral.

Role até o final da página onde diz "Seus aplicativos".

Clique no ícone </> (Web).

Dê um apelido ao app (ex: Painel Web) e clique em Registrar app.

Vai aparecer um código com const firebaseConfig = { ... };.

COPIE apenas o trecho entre as chaves { ... } (incluindo as chaves). Exemplo do que deve copiar:

{
  apiKey: "AIzaSy...",
  authDomain: "painel-otica.firebaseapp.com",
  projectId: "painel-otica",
  storageBucket: "painel-otica.appspot.com",
  messagingSenderId: "123456...",
  appId: "1:123456..."
}


📝 Parte 3: Atualizar o Código HTML

Agora precisa de colocar essas chaves no ficheiro index.html que está no seu computador.

Abra o seu ficheiro index.html (ou OpticalConsultantDashboard.html) com um editor de texto (Bloco de Notas, VS Code, etc).

Procure por esta linha (quase no início do script):

const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');


APAGUE essa linha inteira e substitua pelo código que copiou do Firebase, adicionando const firebaseConfig =  antes. Deve ficar assim:

// Cole aqui a SUA configuração do Firebase
const firebaseConfig = {
  apiKey: "SUA_API_KEY_AQUI",
  authDomain: "SEU_PROJETO.firebaseapp.com",
  projectId: "SEU_PROJECT_ID",
  storageBucket: "SEU_BUCKET...",
  messagingSenderId: "SEU_ID...",
  appId: "SEU_APP_ID..."
};
const appId = 'painel-otica-v1'; // Pode inventar um nome aqui


Salve o ficheiro.

☁️ Parte 4: Publicar no GitHub

Agora que o código tem as chaves da "Sua Casa" (seu banco de dados), pode publicá-lo.

Vá ao GitHub.com e crie um novo repositório (botão "New").

Nome: painel-consultor.

Público.

Clique em "Create repository".

Na página seguinte, clique em "uploading an existing file".

Arraste o seu ficheiro index.html (já editado com as chaves) para lá.

Em baixo, clique em "Commit changes".

Vá a Settings (aba superior) > Pages (menu lateral).

Em Branch, mude de None para main e clique em Save.

🎉 Pronto! Em alguns minutos, o GitHub vai gerar o link do seu site.
Quando acessar e criar uma conta, os dados serão salvos no seu projeto Firebase, totalmente seguro e privado.
