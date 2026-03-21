<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Loja Profissional</title>

<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js"></script>

<style>
body{
  font-family:Arial;
  background:#f5f5f5;
}

button{
  background:#d65a6f;
  color:#fff;
  border:none;
  padding:10px;
  border-radius:8px;
}
</style>
</head>

<body>

<h2>Loja</h2>

<button onclick="login()">Entrar com Google</button>

<div id="produtos"></div>

<script>

// CONFIG FIREBASE (VOCÊ VAI COLOCAR O SEU)
const firebaseConfig = {
  apiKey: "SUA_CHAVE",
  authDomain: "SEU_DOMINIO",
  projectId: "SEU_ID"
};

firebase.initializeApp(firebaseConfig);

const db = firebase.firestore();

// LOGIN
function login(){
  const provider = new firebase.auth.GoogleAuthProvider();
  firebase.auth().signInWithPopup(provider);
}

// LISTAR PRODUTOS
db.collection("produtos").onSnapshot(snapshot => {
  let html = "";

  snapshot.forEach(doc => {
    const p = doc.data();

    html += `
      <div>
        <img src="${p.imagem}" width="100%">
        <h3>${p.nome}</h3>
        <p>R$ ${p.preco}</p>
        <button>Comprar</button>
      </div>
    `;
  });

  document.getElementById("produtos").innerHTML = html;
});

</script>

</body>
</html>
