# Kaler Dairy Farm — शुरू करने की आसान हिंदी गाइड

## पहले जान लें
यह एक बेहतर वेबसाइट प्रोजेक्ट है, लेकिन **सिर्फ GitHub पर अपलोड करने से वेबसाइट का बैकएंड, पेमेंट, ईमेल, WhatsApp और कूरियर की लाइव ट्रैकिंग अपने-आप चालू नहीं होती**। इसके लिए Node.js होस्टिंग, सुरक्षित environment variables, डेटाबेस और संबंधित सेवाओं के अकाउंट/कुंजियाँ चाहिए। इस ZIP में आपकी कोई पेमेंट सीक्रेट या बैंक पासवर्ड नहीं है।

## लोकल कंप्यूटर पर चलाने के चरण
1. ZIP को Extract करें।
2. कंप्यूटर में Node.js 20 या नया वर्ज़न इंस्टॉल करें।
3. Extract किए गए `kaler-dairy-farm-ultimate` फ़ोल्डर में Terminal / Command Prompt खोलें।
4. `npm install` चलाएँ।
5. `.env.example` की कॉपी बनाकर उसका नाम `.env` रखें।
6. अपनी पसंद का मजबूत पासवर्ड अपने कंप्यूटर पर चुनें और उसका hash बनाने के लिए यह कमांड चलाएँ:
   `node -e "require('bcryptjs').hash('APNA-UNIQUE-STRONG-PASSWORD',12).then(console.log)"`
   `APNA-UNIQUE-STRONG-PASSWORD` को अपने पासवर्ड से बदलें। पासवर्ड चैट या GitHub में न डालें।
7. कमांड से निकला hash `.env` में `OWNER_PASSWORD_HASH=` के बाद डालें।
8. `JWT_SECRET` में कम-से-कम 32 अक्षरों की random secret value रखें। इसे सार्वजनिक न करें।
9. `npm start` चलाएँ।
10. ब्राउज़र में `http://localhost:3000` खोलें।

### पेज
- ग्राहक वेबसाइट: `/`
- Owner Dashboard: `/admin.html`
- Employee Portal: `/employee.html`
- Order Tracking: `/track.html`

## Dashboard से
- प्रोडक्ट जोड़/हटा/बदल सकते हैं।
- कीमत, छूट, स्टॉक और seasonal price values बदल सकते हैं।
- तस्वीरों के लिए HTTPS image URLs डाल सकते हैं।
- ऑर्डर की स्थिति, कूरियर का नाम और असली HTTPS tracking link डाल सकते हैं।
- delivery charges और banner बदल सकते हैं।
- कर्मचारी अकाउंट और कुछ permissions बना सकते हैं।

## लाइव करने से पहले आवश्यक काम
- Razorpay व्यापारी अकाउंट और test/live API keys; पेमेंट वेबहुक को production-ready बनाना।
- स्थायी managed database और backups लगाना (अभी starter JSON file का उपयोग करता है)।
- ईमेल SMTP, WhatsApp Business Cloud API और customer message templates कॉन्फ़िगर करना।
- कर्मचारी OTP/MFA जोड़ना।
- कूरियर से API/लाइव ट्रैकिंग एक्सेस लेना।
- वास्तविक उत्पादों की अपनी तस्वीरें, असली कीमतें, उपलब्धता और delivery zones अपडेट करना।
- HTTPS, privacy policy, terms, refund/cancellation policy और production security review पूरा करना।

**सुरक्षा:** `.env` और `data/store.json` को GitHub पर कभी अपलोड न करें। असली भुगतान केवल पेमेंट गेटवे की verified confirmation के बाद ही paid दिखना चाहिए।
