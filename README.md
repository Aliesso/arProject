# arProject

# AR Layihə: şəkli skan edəndə 3D fiqur

Kamera müəyyən bir şəkli (hədəfi) görəndə həmin şəklin üzərində 3D fiqur çıxır.
Texnologiya: [MindAR](https://github.com/hiukim/mind-ar-js) + [A-Frame](https://aframe.io) (brauzerdə işləyir, tətbiq yükləmək lazım deyil).

## 1. Test (hazır nümunə şəkli ilə)

1. Bu hədəf şəkli kompüter ekranında açın və ya çap edin:
   https://cdn.jsdelivr.net/gh/hiukim/mind-ar-js@1.2.5/examples/image-tracking/assets/card-example/card.png
2. Layihəni işə salın (aşağıya baxın) və telefonda / kompüterdə açın.
3. Kameranı şəklə tutun və 3D fiqurlar görünəcək.

## 2. İşə salmaq

Kamera yalnız **HTTPS** və ya **localhost** üzərində işləyir.

**Kompüterdə (localhost):**
```bash
npx http-server -p 8080
```
Sonra `http://localhost:8080` açın.

**Telefonda:** HTTPS lazımdır. Ən asan yollar:
- `npx http-server -S -C cert.pem -K key.pem` (öz sertifikatınızla), və ya
- `npx localtunnel --port 8080` / `ngrok http 8080` ilə HTTPS link alın, və ya
- layihəni GitHub Pages / Netlify-a yükləyin.

## 3. Öz şəklinizi hədəf etmək

1. https://hiukim.github.io/mind-ar-js-doc/tools/compile açın.
2. Öz şəklinizi (afişa, loqo, kitab üzü və s.) yükləyin və **Start** basın.
3. `targets.mind` faylını endirib bu qovluğa qoyun.
4. `index.html`-də `imageTargetSrc` dəyərini dəyişin:
   ```html
   mindar-image="imageTargetSrc: ./targets.mind; ..."
   ```

Yaxşı hədəf şəkli üçün: çoxlu detal, kontrast, təkrarlanmayan naxış. Düz rəngli və ya sadə şəkillər pis tanınır.

## 4. Öz 3D modelinizi qoymaq

1. `.glb` və ya `.gltf` modeli (məs. [Sketchfab](https://sketchfab.com)-dan) `models/` qovluğuna qoyun.
2. `index.html`-də:
   ```html
   <a-asset-item id="car" src="./models/model.glb"></a-asset-item>
   ```
3. Ölçü və mərkəzləmə avtomatikdir: `fit-model="size: 0.75"` modeli şəklin eninin 75%-nə gətirir
   (hədəf şəklinin eni = 1 vahid). `remove: Fabric` hissəsini yeni model üçün silin.

Hazırkı model: [Toy Car](https://github.com/KhronosGroup/glTF-Sample-Assets/tree/main/Models/ToyCar), Guido Odendahl, CC0 (pulsuz).

## 5. Bir neçə şəkil, fərqli fiqurlar

Kompilyatora bir neçə şəkil yükləyin, sonra hər şəkil üçün ayrıca hədəf yazın:
```html
<a-entity mindar-image-target="targetIndex: 0"> ...1-ci şəklin fiquru... </a-entity>
<a-entity mindar-image-target="targetIndex: 1"> ...2-ci şəklin fiquru... </a-entity>
```
Və `mindar-image`-ə `maxTrack: 2` əlavə edin.
