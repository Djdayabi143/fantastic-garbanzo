<!DOCTYPE html>
<html lang="or">
<head>
  <meta charset="UTF-8">
  <title>ଫଟୋରୁ ପୃଷ୍ଠଭୂମି ହଟାନ୍ତୁ - Odia Background Remover</title>
  <meta name="description" content="ଏଠାରେ ଏକ କ୍ଲିକ୍ ରେ ଫଟୋରୁ ପୃଷ୍ଠଭୂମି ହଟାନ୍ତୁ | PNG ଡାଉନଲୋଡ୍ କରନ୍ତୁ | Made by Dayanidhi Jena">
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 2rem;
      background: #f0f8ff;
    }
    h1 {
      color: #007f5f;
    }
    input, button {
      margin: 1rem;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 8px;
    }
    button {
      background-color: #0284c7;
      color: white;
      border: none;
    }
    img {
      margin-top: 20px;
      max-width: 90%;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }
    a {
      display: block;
      margin-top: 10px;
      font-size: 18px;
    }
    footer {
      margin-top: 3rem;
      color: #555;
    }
  </style>
</head>
<body>
  <h1>ଫଟୋରୁ ପୃଷ୍ଠଭୂମି ହଟାନ୍ତୁ</h1>
  <p>ଏଠାରେ ଏକ ଫଟୋ ଅପଲୋଡ୍ କରନ୍ତୁ, ଆମେ ଆପଣଙ୍କ ପାଇଁ ପୃଷ୍ଠଭୂମି ହଟାଇଦେବୁ</p>
  <input type="file" id="imageUpload" accept="image/*">
  <button onclick="removeBackground()">ପୃଷ୍ଠଭୂମି ହଟାନ୍ତୁ</button>
  <div>
    <img id="resultImage" style="display:none;" />
    <a id="downloadLink" style="display:none;" download="removed-background.png">PNG ଡାଉନଲୋଡ୍ କରନ୍ତୁ</a>
  </div>
  <footer>© 2025 Made with ❤️ in Odisha by Dayanidhi Jena</footer>

  <script>
    async function removeBackground() {
      const fileInput = document.getElementById('imageUpload');
      if (!fileInput.files.length) return alert("ଦୟାକରି ଫଟୋ ବାଛନ୍ତୁ");

      const formData = new FormData();
      formData.append("image", fileInput.files[0]);

      const response = await fetch("/remove-bg", {
        method: "POST",
        body: formData,
      });

      if (!response.ok) {
        alert("ପୃଷ୍ଠଭୂମି ହଟାଇବାରେ ତ୍ରୁଟି ହେଲା");
        return;
      }

      const blob = await response.blob();
      const url = URL.createObjectURL(blob);
      document.getElementById("resultImage").src = url;
      document.getElementById("resultImage").style.display = "block";
      const link = document.getElementById("downloadLink");
      link.href = url;
      link.style.display = "block";
    }
  </script>
</body>
</html>
