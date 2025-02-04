<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أنا هنا</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; direction: rtl; }
        #preview img { margin-top: 20px; width: 100%; max-width: 400px; }
        input { padding: 10px; margin: 10px; font-size: 18px; }
        button { padding: 10px 20px; font-size: 18px; cursor: pointer; }
    </style>
</head>
<body>
    <h2>اكتب اسمك لتحصل على صورة المشاركة</h2>
    <input type="text" id="nameInput" placeholder="اكتب اسمك هنا">
    <button onclick="generateImage()">إنشاء الصورة</button>
    <br><br>
    <canvas id="canvas" width="600" height="400" style="display:none;"></canvas>
    <div id="preview"></div>

    <script>
        function generateImage() {
            const name = document.getElementById('nameInput').value.trim();
            if (!name) { alert("يرجى إدخال الاسم!"); return; }

            const canvas = document.getElementById('canvas');
            const ctx = canvas.getContext('2d');

            // إضافة الصورة كخلفية
            const backgroundImg = new Image();
            backgroundImg.src = 'https://dl.dropboxusercontent.com/scl/fi/g4fvftq31uuej9jwb0xdj/IMG_3465.png?rlkey=sk9kmaw4x1th5s644zov9chgl&st=eg0d0b9e&dl=0'; // رابط الصورة المعدل
            backgroundImg.onload = function() {
                ctx.drawImage(backgroundImg, 0, 0, canvas.width, canvas.height);

                // نص "أنا هناك"
                ctx.fillStyle = "#000";
                ctx.font = "bold 40px Arial";
                ctx.fillText("أنا هناك", 220, 50);

                // إضافة اسم المستخدم
                ctx.font = "30px Arial";
                ctx.fillText(name, 250, 200);

                // تحويل إلى صورة
                const img = new Image();
                img.src = canvas.toDataURL();
                img.onload = function() {
                    document.getElementById('preview').innerHTML = "";
                    document.getElementById('preview').appendChild(img);

                    // زر تحميل الصورة
                    const downloadLink = document.createElement("a");
                    downloadLink.href = img.src;
                    downloadLink.download = "أنا_هنا.png";
                    downloadLink.innerText = "تحميل الصورة";
                    document.getElementById('preview').appendChild(document.createElement("br"));
                    document.getElementById('preview').appendChild(downloadLink);
                };
            };
        }
    </script>
</body>
</html>
