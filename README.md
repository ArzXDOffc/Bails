# WhatsApp Baileys @ArzXDFvck

<p align="center">
  <img src="https://h.top4top.io/p_35995wdvx1.jpg" alt="Thumbnail" width="500"/>
</p>

**WhatsApp Baileys** adalah library open‑source yang dirancang untuk membantu developer membangun solusi otomatisasi dan integrasi dengan WhatsApp secara efisien. Menggunakan teknologi *webclient* tanpa memerlukan browser, library ini mendukung berbagai fitur seperti manajemen pesan, penanganan chat, administrasi grup, serta pesan interaktif untuk pengalaman pengguna yang lebih dinamis.

Aktif dikembangkan dan dipelihara, library ini terus menerima pembaruan untuk meningkatkan stabilitas dan performa. Salah satu fokus utamanya adalah menyempurnakan proses pairing dan autentikasi agar lebih stabil dan aman.

---

### 🚀 Fitur Utama dan Keunggulan

* **Pairing Stabil:** Mendukung proses pairing otomatis dan kustom dengan perbaikan pada masalah *disconnect*.
* **Pesan Interaktif:** Mendukung *native flow*, tombol aksi, menu dinamis, dan pesan album.
* **Multi-Device:** Kompatibel dengan fitur multi-device terbaru WhatsApp.
* **Manajemen Sesi:** Penanganan sesi yang efisien dan andal menggunakan `sock`.
* **Ringan & Modular:** Performa tinggi tanpa beban berat dari engine browser, mudah diintegrasikan.

---

## 🛠 Dokumentasi SendMessage

Gunakan instance `sock` untuk memanggil fungsi-fungsi di bawah ini.

### 1. Order Message
```javascript
await sock.sendMessage(groupId, {
    orderMessage: {
        orderId: "7778",
        thumbnail: await (await fetch("URL IMG")).buffer(),
        itemCount: 1000,
        status: "INQUIRY",
        surface: "CATALOG",
        message: "ArzXDFvck kimochi",
        orderTitle: "kyah",
        sellerJid: "0@s.whatsapp.net",
        token: Buffer.from("777777"),
        totalAmount1000: 1000,
        currencyCode: "IDR",
        messageVersion: 2
    }
}, { quoted: m });
```

------------------------------

### 2. Riview And Pay Message
```JavaScript
await sock.sendMessage(m.chat, {
    nativeFlowMessage: {
        buttons: [{
            name: "review_and_pay",
            buttonParamsJson: JSON.stringify({
                currency: "IDR",
                total_amount: { value: 100, offset: 100 },
                reference_id: "ArzXDFvck-DEV",
                type: "ArzXDFvck",
                payment_status: "ganteng",
                payment_timestamp: Date.now(),
                order: {
                    status: "completed",
                    subtotal: { value: 100, offset: 100 },
                    order_type: "PAYMENT_REQUEST",
                    items: [{
                        retailer_id: "item-" + Math.floor(Math.random() * 1e9),
                        name: teks,
                        amount: { value: 100, offset: 100 },
                        quantity: 1
                    }]
                },
                additional_note: "ArzXDFvck gntng bet jir",
                native_payment_methods: "",
                share_payment_status: true
            })
        }]
    }
}, { quoted: m });
```

------------------------------

### 3. Tag Status Media
```JavaScript
const quoted = m.quoted ? m.quoted : m;
const mime = (quoted.msg || quoted).mimetype || "";
const caption = m.body.replace(/^\.swgrup\s*/i, "").trim();

if (/image/.test(mime)) {
    const buffer = await quoted.download();
    await sock.sendMessage(groupId, { groupStatusMessage: { image: buffer, caption } });
} else if (/video/.test(mime)) {
    const buffer = await quoted.download();
    await sock.sendMessage(groupId, { groupStatusMessage: { video: buffer, caption } });
} else if (/audio/.test(mime)) {
    const buffer = await quoted.download();
    await sock.sendMessage(groupId, { groupStatusMessage: { audio: buffer } });
}
```

------------------------------

### 4. Album Message
```JavaScript
await sock.sendMessage(m.chat, {
    albumMessage: [
        { image: { url: "URL_1" }, caption: "Foto pertama" },
        { image: { url: "URL_2" }, caption: "Foto kedua" }
    ]
}, { quoted: m });
```

------------------------------

### 5. Event & Poll Message
```JavaScript
// Event Message
await sock.sendMessage(m.chat, {
    eventMessage: {
        isCanceled: false,
        name: "ArzXDFvck Project",
        description: "ravage native",
        location: { degreesLatitude: 0, degreesLongitude: 0, name: "ArzXDFvck Base" },
        joinLink: "[https://call.whatsapp.com/video/ArzXDFvck](https://call.whatsapp.com/video/ArzXDFvck)",
        startTime: "1763019000",
        endTime: "1763026200",
        extraGuestsAllowed: false
    }
}, { quoted: m });

// Poll Result Message
await sock.sendMessage(m.chat, {
    pollResultMessage: {
        name: "Hello World",
        pollVotes: [
            { optionName: "ArzXDFvck 1", optionVoteCount: "112233" },
            { optionName: "ArzXDFvck 2", optionVoteCount: "1" }
        ]
    }
}, { quoted: m });
```

------------------------------

### 6. Interactive Message
```JavaScript
await sock.sendMessage(m.chat, {
    interactiveMessage: {
        header: "Hello World",
        title: "ArzXDFvck System",
        footer: "telegram: @ArzXDFvck",
        image: { url: "[https://example.com/image.jpg](https://example.com/image.jpg)" },
        nativeFlowMessage: {
            messageParamsJson: JSON.stringify({
                limited_time_offer: {
                    text: "Special Offer",
                    url: "[https://t.me/ArzXDFvck](https://t.me/ArzXDFvck)",
                    copy_code: "ravage",
                    expiration_time: Date.now() * 999
                },
                bottom_sheet: {
                    list_title: "ravage native",
                    button_title: "pilih di sini"
                }
            }),
            buttons: [
                {
                    name: "cta_copy",
                    buttonParamsJson: JSON.stringify({
                        display_text: "copy code",
                        id: "123456789",
                        copy_code: "ARZX-CODE"
                    })
                }
            ]
        }
    }
}, { quoted: m });
```

------------------------------

### 7. Document Interactive Message
```JavaScript
await sock.sendMessage(m.chat, {
    interactiveMessage: {
        header: "File Sharing",
        title: "ArzXDFvck Docs",
        footer: "telegram: @ArzXDFvck",
        document: fs.readFileSync("./package.json"),
        mimetype: "application/pdf",
        fileName: "ArzXDFvck.pdf",
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Join Telegram",
                    url: "[https://t.me/ArzXDFvck](https://t.me/ArzXDFvck)"
                })
            }
        ]
    }
}, { quoted: m });
```

------------------------------

### 8. Request Payment Message
```JavaScript
let quotedContent = JSON.stringify({ [m.quoted?.mtype]: m.quoted }, null, 2);

await sock.sendMessage(m.chat, {
    requestPaymentMessage: {
        currency: "IDR",
        amount: 10000000,
        from: m.sender,
        sticker: JSON.parse(quotedContent),
        background: {
            id: "100",
            width: 1000,
            height: 1000,
            mimetype: "image/webp",
            placeholderArgb: 0xFF00FFFF,
            textArgb: 0xFFFFFFFF
        }
    }
}, { quoted: m });
```

------------------------------


## Mengapa Memilih WhatsApp Baileys?

Karena library ini menawarkan stabilitas tinggi, fitur lengkap, dan proses pairing yang terus ditingkatkan. Ideal bagi developer yang ingin membuat solusi otomatisasi WhatsApp yang profesional dan aman. Dukungan terhadap fitur terbaru WhatsApp memastikan kompatibilitas dengan pembaruan platform.

------------------------------

### Catatan Teknis

- Mendukung pairing code kustom yang stabil dan aman
- Memperbaiki masalah terkait pairing dan autentikasi pada versi sebelumnya
- Fitur pesan interaktif dan tombol aksi untuk membuat menu dinamis
- Manajemen sesi otomatis yang efisien untuk stabilitas jangka panjang
- Kompatibel dengan fitur multi-device terbaru WhatsApp
- Mudah diintegrasikan dan dikustomisasi sesuai kebutuhan
- Sempurna untuk mengembangkan bot, otomatisasi layanan pelanggan, dan aplikasi komunikasi lainnya

------------------------------

Untuk dokumentasi lengkap, panduan instalasi, dan contoh implementasi, silakan kunjungi repository resmi dan forum komunitas. Kami terus memperbarui dan meningkatkan library ini untuk memenuhi kebutuhan developer dan pengguna solusi otomatisasi WhatsApp modern.

**Terima kasih telah memilih WhatsApp Baileys sebagai solusi otomatisasi WhatsApp Anda!**
