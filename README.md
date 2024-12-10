<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Book Customizer</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    form { max-width: 500px; margin: auto; }
    .preview { margin-top: 20px; }
    button { background-color: #4CAF50; color: white; border: none; padding: 10px 20px; cursor: pointer; }
  </style>
</head>
<body>
  <h1>Créer un livre personnalisé</h1>
  <form id="bookForm">
    <label for="title">Titre du livre :</label>
    <input type="text" id="title" name="title" required><br><br>
    
    <label for="theme">Thème :</label>
    <input type="text" id="theme" name="theme" required><br><br>
    
    <label for="story">Script de l'histoire :</label><br>
    <textarea id="story" name="story" rows="5" cols="40" required></textarea><br><br>
    
    <button type="submit">Générer</button>
  </form>
  <div class="preview" id="preview"></div>

  <script>
    document.getElementById('bookForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      const title = document.getElementById('title').value;
      const theme = document.getElementById('theme').value;
      const story = document.getElementById('story').value;
      
      // Call the backend API to generate the book preview
      const response = await fetch('/generate', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ title, theme, story })
      });
      
      const data = await response.json();
      document.getElementById('preview').innerHTML = `
        <h2>Aperçu :</h2>
        <img src="${data.cover}" alt="Couverture du livre" style="width:200px"><br>
        <p>${data.summary}</p>
        <button onclick="window.location.href='${data.downloadUrl}'">Télécharger</button>
        <button onclick="alert('Impression à venir !')">Imprimer</button>
      `;
    });
  </script>
</body>
</html>
