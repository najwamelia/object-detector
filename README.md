# object_detector

Kami menggunakan referensi dari nanonets yang menggunakan tensorflowjs atau yang versi javascript dan framework vue. Selain itu juga menggunakan model coco ssd yang bisa mendeteksi sekitar 80 objek secara ssd atau single shot multiple detection.

1. Instal vue untuk projek object-detection (buat folder object-detection)
2. Masuk ke directory projeknya, lalu instal tensorflowjs dengan command "npm install @tensorflow/tfjs"
3. Instal model coco ssd dengan command "nmp install @tensorflow-models/coco-ssd"
4. Coding program dalam app.vue
5. Jalankan scriptnya dengan command npm run serve
6. Masuk ke browser dengan url localhost 8080 


# Penjelasan:
1. Disini kami mengerjakan program coding-nya dalam app.vue
2. Dalam template, membuat elemen video yang autoplay, muted, plays in line, bind dengan camera, nah cameranya width 640, dan height 480, idnya cam, style position fixed, top 50px
2. Elemen selanjutnya yaitu canvas untuk merender objeknya dengan id c, widht, height, dan style sama seperti video.
3. Lalu kami membuat script javascriptnya,
pertama import tensorflow/tfjs dan cocossd nya
4. Kemudian menggunakan compositon api dari vue
5. Setup, kami buat variabel camera yang reactive di dalamnya ada srcObject yang akan menampung gambar kamera
6. Lalu buat variabel constraint yang menunjukkan kalau kami tidak menggunakan audionya tapi video saja
7. Kemudian variabel webcam yang asinkronus, dengan try catch yang akan meng assign value dari camera (srcObject) dan await navigator.mediaDevices.getUserMedia(contraint) untuk memanggil webcam lalu disimpan ke srcObject. Lalu await camera.onloadmetadata untuk menunggu metadatanya ada baru ditampilkan. Kemudian di console log agar jika ada error tidak membingungkan.
8. Lalu buat variabel load yang asyncronus. disini untuk menunggu webcamnya terload dan modelnya cocoSsd dengan base default modilnet_v2     
9. Selanjutnya cam = document.getElementById"cam" diambil cam untuk mendetek dari videoframe dengan mempassing loadmodel, dan cam. 
10. Fungsi detectFromVideoFrame isinya model dan video,  jadi ketika model mendeteksi video, maka akan dapat prediction objectnya apa saja. Kemudian ditampilkan predictionnya, dan requestAnimationFram agar terus berulang.
11. Fungsi showdetection dengan parameter prediction yang dipassing untuk menampilkan kotak hijau sebagai penanda ketika ada object dicamera. Pertama get element id canvas, lalu ambil konteksnya canvas 2d, lalu clearRect dan kita definisikan fontnya serta contextnya di top
12. Selanjutnya for each prediction, akan didapatkan koordinatnya x dan y dengan value array jadi mendapatkan properti dari setiap objek yang dideteksi,
13. Strokestyle untuk warna kotaknya, fillstyle untuk warna dari kotak tulisannya
14. let preditionText = prediction.class jadi hasil prediksi akan didapat dari prediction class dan disimpan di predictionText 
16. onMounted untuk meload camera dan modlenya, jika ada device untuk mengambil media maka kita panggil fungsi load, else berarti devicenya not supported
15. Terakhir kita kembalikan atau return camera
