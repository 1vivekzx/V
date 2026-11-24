# V Browser: APK Builder (हिंदी गाइड)

इस ZIP से आप अपनी **V Browser वेबसाइट** का Android APK GitHub पर बना सकते हैं। वेबसाइट APK के **अंदर** रखी जाती है और ऐप उसे अपने अंदर से खोलता है (Supabase login/sync पहले की तरह चलता है)।

आपके पास **दो ZIP** हैं:

| ZIP | इसमें क्या है |
|---|---|
| `V-Browser-Website.zip` | आपकी पूरी वेबसाइट, जैसी थी वैसी (`index.html`, `README.txt`) |
| `V-Browser-APK-Builder.zip` | Android Studio project, WebView का Java code, Gradle files, GitHub workflow, ये README |

---

## 1. दोनों ZIP को जोड़ना (extract करके)

1. `V-Browser-APK-Builder.zip` को **extract** करें। आपको ये मिलेगा:
   ```
   .github/workflows/build-apk.yml
   app/
   gradle/
   keystore/
   website/            ← ये folder अभी लगभग खाली है
   WORKFLOW-COPY/build-apk.yml
   build.gradle
   settings.gradle
   gradle.properties
   .gitignore
   README-HINDI.md
   ```
2. `V-Browser-Website.zip` को **extract** करें। आपको `index.html` और `README.txt` मिलेंगी।
3. उन दोनों फ़ाइलों (`index.html`, `README.txt`) को **`website` folder के अंदर** रख दें। यानी:
   ```
   website/index.html
   website/README.txt
   ```
   अगर extract करने पर एक अलग folder बन गया (जैसे `V-Browser-Website/index.html`), तो वो folder `website` के अंदर रख दें तब भी चलेगा (`website/V-Browser-Website/index.html`)। workflow `index.html` खुद ढूँढ लेता है।
4. अब आपका पूरा project तैयार है। ऊपर वाली सारी चीज़ें (`app`, `gradle`, `keystore`, `website`, `.github`, `build.gradle`, `settings.gradle`, `gradle.properties`, `.gitignore`, `README-HINDI.md`) **एक ही folder में एक साथ** होनी चाहिए। उस folder का नाम कुछ भी हो सकता है।

> ध्यान: `website` folder का नाम छोटे अक्षरों में `website` ही रखें। `index.html` का नाम भी बिल्कुल यही रहे।

---

## 2. GitHub पर upload करना

### तरीका A: कंप्यूटर (PC) से (सबसे आसान)
1. GitHub पर नई repository बनाएँ (**Private** रखना बेहतर है) और खोलें।
2. **Add file → Upload files** दबाएँ।
3. ऊपर बताए पूरे project folder के **अंदर की सारी चीज़ें** (folder समेत) खींचकर (drag) वहाँ छोड़ दें। ज़रूरी: `.github` folder भी जाए। अगर PC पर `.github` दिखता नहीं तो file manager में "Show hidden files" चालू करें।
4. सब upload होने के बाद नीचे **Commit changes** दबाएँ।
5. Repository के पहले पन्ने पर जाँचें कि ये सब दिख रहे हैं: `.github`, `app`, `gradle`, `keystore`, `website`, `build.gradle`, `settings.gradle`, `gradle.properties`।

### तरीका B: सिर्फ़ फ़ोन से (folders upload नहीं होते, इसलिए ये तरीका)
फ़ोन के Chrome से GitHub में folder चुनकर upload नहीं किया जा सकता। इसके लिए workflow में एक आसान रास्ता रखा गया है:

1. GitHub पर नई repository बनाएँ।
2. **Add file → Upload files** में सिर्फ़ ये **दो ZIP** (बिना extract किए) upload करें और Commit करें:
   - `V-Browser-APK-Builder.zip`
   - `V-Browser-Website.zip`
3. अब workflow की फ़ाइल बनानी है: **Add file → Create new file**। नाम वाली जगह यही लिखें (slash `/` लिखते ही folders अपने-आप बन जाते हैं):
   ```
   .github/workflows/build-apk.yml
   ```
4. Builder ZIP में `WORKFLOW-COPY/build-apk.yml` फ़ाइल है (दिखने वाले folder में)। उसे खोलकर **पूरा text copy** करें और यहाँ paste करें। फिर **Commit changes** दबाएँ।
5. आगे का तरीका एक जैसा है (नीचे भाग 3)। Workflow दोनों ZIP को खुद extract करके जोड़ लेगा।

> नाम में "builder" और "website" शब्द होना ज़रूरी है (जैसे `V-Browser-APK-Builder.zip`, `V-Browser-Website.zip`)।

---

## 3. APK बनाना (GitHub Actions)

1. Repository में ऊपर **Actions** tab खोलें। अगर "I understand my workflows, go ahead and enable them" दिखे तो वो बटन दबाएँ।
2. बाईं तरफ़ **Build V Browser APK** पर tap करें।
3. दाईं तरफ़ **Run workflow** दबाएँ, फिर हरे **Run workflow** बटन पर tap करें।
4. कुछ सेकंड में एक पीली गोल निशान वाली run दिखेगी। लगभग **6 से 12 मिनट** में ये हरी ✔ हो जाएगी।
5. उस run पर tap करें। नीचे **Artifacts** में **V-Browser-APK** दिखेगा। उस पर tap करके download करें। (GitHub इसे ZIP में देता है। उसे extract करके अंदर से `V-Browser.apk` निकालें।)
6. `V-Browser.apk` फ़ोन में खोलकर install करें। "Unknown apps / अज्ञात स्रोत" की अनुमति माँगे तो दे दें।

### अगर Play Protect चेतावनी दे
ये Google Play के बाहर से install होने वाले हर ऐप पर आ सकती है। **More details → Install anyway** दबाएँ। "Scan app" का विकल्प हो तो पहले वही दबाएँ।

---

## 4. वेबसाइट बदलनी हो तो
1. GitHub में `website/index.html` खोलें, ✏️ (Edit) से बदलें (या नई फ़ाइल upload करके पुरानी की जगह रखें), Commit करें।
2. Actions में दोबारा **Run workflow** चलाएँ और नया APK download करें।
3. नया APK पुराने ऐप के ऊपर install हो जाएगा (signing key वही रहती है, इसलिए पुराना ऐप हटाने की ज़रूरत नहीं)।

---

## 5. अगर build fail हो जाए
Actions में उस run पर tap करें। ऊपर **लाल box** में error का text दिखेगा। सबसे आम कारण:

| संदेश | मतलब और हल |
|---|---|
| `website folder nahi mila` | Repository में `website` folder नहीं पहुँचा। भाग 1 और 2 दोबारा देखें। |
| `index.html nahi mili` | `website` folder खाली है। `V-Browser-Website.zip` की फ़ाइलें उसके अंदर डालें। |
| `Project nahi mila` | भाग 2 के तरीका B में Builder ZIP का नाम "builder" वाला नहीं है, या ZIP पहुँची नहीं। |
| कोई और error | उस लाल box का text (या screenshot) भेज दें। |

Run के पन्ने पर **build-log** नाम का download भी मिलता है, जिसमें पूरा log है।

---

## 6. ऐप कैसे काम करता है (संक्षेप में)
- वेबसाइट APK के `assets/website/` में रखी जाती है और ऐप में `https://appassets.androidplatform.net/assets/website/index.html` से खुलती है। (ये Android का अपना सुरक्षित पता है, इंटरनेट पर कोई साइट नहीं।)
- **Supabase** का URL और key आपके `index.html` में ही हैं। मैंने उसमें कुछ नहीं बदला, इसलिए login, bookmarks और history sync पहले जैसा चलता है।
- वेबसाइट Supabase की library इंटरनेट से (jsDelivr CDN) लेती है, इसलिए **ऐप को इंटरनेट चाहिए**। इंटरनेट के बिना login और sync नहीं चलेगा।
- ऐप में लिंक बाहर के किसी दूसरे browser में नहीं खुलते। बुकमार्क पर tap करने से वो V Browser के अंदर ही खुलता है।
- Fullscreen video, JavaScript alert/confirm (जैसे "History मिटाएँ?") और downloads चलते हैं। कैमरा, माइक और लोकेशन की अनुमति embedded साइटों को नहीं दी जाती।

## 7. सीमाएँ (ईमानदारी से)
- कई साइटें (जैसे Google, Facebook, बैंक) दूसरे पन्ने के अंदर खुलने (iframe) से मना करती हैं। ये वही सीमा है जो आपकी वेबसाइट के `README.txt` में लिखी है; ऐप में भी वही रहेगी, क्योंकि वेबसाइट बदली नहीं गई है।
- ← → बटन cross-site iframe में काम नहीं करते (ब्राउज़र की सुरक्षा), जैसे वेबसाइट पर भी।
- APK की signing key (`keystore/vbrowser-release.jks`, पासवर्ड `vbrowser123`) इस project में ही रखी है ताकि हर build उसी key से बने। ये सिर्फ़ निजी इस्तेमाल के लिए ठीक है। Google Play पर डालना हो तो अपनी अलग key बनानी होगी, और repository **Private** रखें।

## 8. Android Studio में खोलना (वैकल्पिक)
Android Studio (JDK 17) में इस folder को **Open** करें। पहले `website` folder में अपनी फ़ाइलें रखें। Studio Gradle 8.9 download करने को कहेगा। फिर **Build → Build APK(s)**।

## तकनीकी जानकारी
- Android Gradle Plugin 8.5.2, Gradle 8.9, JDK 17, compileSdk/targetSdk 34, minSdk 24 (Android 7.0 और ऊपर)
- Package: `com.vivek.vbrowser`, Java source: `app/src/main/java/com/vivek/vbrowser/MainActivity.java`
- `androidx.webkit` (WebViewAssetLoader) सिर्फ़ एक dependency है
