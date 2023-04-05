---
layout: page
order: 5
---

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Random Image</title>
  </head>
  <body>
    <h1>Random Image</h1>
    <img id="myImage" src="">
    <script>
      var images = [
        "https://memes.us-east-1.linodeobjects.com/auger/12 Emotes of SimpleCyberMas.png",
        "https://memes.us-east-1.linodeobjects.com/auger/AbeAuger.png",
        "https://memes.us-east-1.linodeobjects.com/auger/BabyGerryNewYear.png"
      ];
      var randomIndex = Math.floor(Math.random() * images.length);
      var randomImage = images[randomIndex];
      document.getElementById("myImage").src = randomImage;
    </script>
  </body>
</html>