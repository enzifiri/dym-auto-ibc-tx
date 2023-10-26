# dym-auto-ibc-tx
Keplr > Metamask IBC TRANSFER for MONKEYS! (rollapes)

## 1-Keplrdan Geliştiric modunu açalım. Sırasıyla işaretlediğim yerlere basın.
![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/72327bc4-4078-4a6a-9945-c6892f931ecd)


## 2-Şimdi Roll Applerin ağlarını cüzdanımıza ekleyeceğiz (IBC transfer kısmında lazım olacak), Alttaki Linke girin ve Deposit Funds butonuna basın, Keplrdan Keplra gönderimi seçin. Sırasıyla işaretledğim butonlara baısn
https://portal.dymension.xyz/rollapp/rues_2215298-1
![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/354b75c4-8322-4e2b-ae1b-5ad57114578f)


## 3-Altta verdiğim urlyi tarayıcınızda yeni sekme açıp aratın. Sonrasında en alttaki Advanced IBC ksımındaki Transfer butonuna basın.

URL: chrome-extension://dmkamcknogkgcdfhhbddcghachkejeap/popup.html

![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/51b8a444-620e-49b8-a21d-77f0378ae5f3)


## 4-DYM tokeni seçin ve Desnation chain kısmına basın en altta New IBC Trasnfer channele basın. Alttaki gibi karşılıklı TX yapacağımız kişilerin ağını eklememiz gerekiyor. Destination chain: Rues_221.... Channel: 6195, Bilgileri girdikten sonra save diyip kaydedin.
![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/8393cb2e-829b-4dc6-9c46-c1cf3f11d8ed)


## 5-Wallet addres kısmına hangi rollup olursa olsun aynı adresi gireceğiz, Çünkü IBC transferi yapmak için adres bu, channel ile de hangi rollupa işlem göndereceğimizi belirledik. Adresi girip Next butonuna basın.

adress: ethm1hmssffakpll0d3hesk2j8s286zd9yfv0pzlcag

![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/7eb183c1-4c93-48af-8de2-3235a861ffb4)


## 6-Sonrasına Amount kısmına istediğinizi yazın ben 0.01 transfer ederek tx kasıyorum. Next butonuna basmadan önce fotoğrafta belirttiğim gibi oluşan URLyi bi yere not edin, TX yapacağımız zaman bu urlyi aratıp hızlıca TX kasabileceğiz.

![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/0e7444f8-0640-4a41-b2bf-34e5264e27b1)


## Keplr kullanarak IBC transfer yapmak bu kadar basit, Bu işlemlerden sonra Otomatik olarak IBC Transfer göndermek için script var, Kimin Rollupunda TX kasacaksanız 2. adımda anlattığım Rollup Ağını ekleyip bunu Keplra tanıtmanız gerekiyor. Scrpitin anlatımına geçeyim.

### window.location.href kısmında kimle tx kasacaksanız onun urlsini değiştirin. Değiştirmeden kullanırsanız Rues_221... kanalında IBC transfer yapacaksınız.
### Kodu kullanmadan alttaki urlye tekrar gidelim sağ tıklayıp incele diyelim, ardından sol üstteki Console butonuna basıp alttaki kodu direk yapıştırıp çalıştırın.
### Not: Sekmeyi arkaplana atarsanız IBC transfer gönderilmiyor, bilgisayarı kullanmadığınız anda açıp Tarayıcınızı arkaplana atmayın.
![image](https://github.com/enzifiri/dym-auto-ibc-tx/assets/76253089/caa32879-73ff-4598-9dc3-244f19c468a1)
### Url: chrome-extension://dmkamcknogkgcdfhhbddcghachkejeap/popup.html

```
async function anaIslem() {
    const bekle = (ms) => new Promise(resolve => setTimeout(resolve, ms));

    while (true) {
        // BASKASINA TRANSFER YAPACAKSANIZ BURDAKİ URLYİ DEĞİŞTİRİN. (default rues_221....)
        window.location.href = 'chrome-extension://dmkamcknogkgcdfhhbddcghachkejeap/popup.html#/ibc-transfer?chainId=froopyland_100-1&coinMinimalDenom=udym&initialGasAdjustment=1.3&initialIBCChannels=%5B%7B%22channelId%22%3A%22channel-6195%22%2C%22counterpartyChainId%22%3A%22rues_2215298-1%22%2C%22portId%22%3A%22transfer%22%7D%5D&initialRecipient=ethm1hmssffakpll0d3hesk2j8s286zd9yfv0pzlcag&initialFeeCurrency=udym&initialFeeType=average&initialAmount=0.01';

        await bekle(1000); // Sayfanın yüklenmesini bekleyin (gerektiğinde süreyi ayarlayın)

        let nextBulundu = false;
        let approveBulundu = false;

        try {
            // İlk Next düğmesine tıkla
            document.querySelector('#app > div > div > div > div.simplebar-wrapper > div.simplebar-mask > div > div > div > div > div.sc-bczRLJ.DypIt > div > div > button').click();
            nextBulundu = true;
        } catch (error) {
            nextBulundu = false;
            console.error('İlk Next düğmesi bulunamadı. Tekrar deneyin.');
        }

        await bekle(1000); // Sayfanın yüklenmesini bekleyin (gerektiğinde süreyi ayarlayın)

        try {
            // İkinci Next düğmesine tıkla
            document.querySelector('#app > div > div > div > div.simplebar-wrapper > div.simplebar-mask > div > div > div > div > div.sc-bczRLJ.DypIt > div > div > button').click();
            nextBulundu = true;
        } catch (error) {
            nextBulundu = false;
            console.error('İkinci Next düğmesi bulunamadı. Tekrar deneyin.');
        }

        await bekle(1000); // Sayfanın yüklenmesini bekleyin (gerektiğinde süreyi ayarlayın)

        try {
            // Approve düğmesine tıkla
            document.querySelector('#app > div > div > div > div.simplebar-wrapper > div.simplebar-mask > div > div > div > div > div.sc-bczRLJ.DypIt > div > button').click();
            approveBulundu = true;
        } catch (error) {
            approveBulundu = false;
        }

        // Eğer "Approve" düğmesi bulunamazsa ve en az bir "Next" düğmesi bulunmuşsa
        if (!approveBulundu && nextBulundu) {
            // Önceki "Next" düğmelerini bulup tıkla
            try {
                document.querySelector('#app > div > div > div > div.simplebar-wrapper > div.simplebar-mask > div > div > div > div > div.sc-bczRLJ.DypIt > div > div > button').click();
            } catch (error) {
                console.error('Önceki "Next" düğmeleri bulunamadı. Tekrar deneyin.');
            }
        }

        // Transaction Success elementini bulana kadar bekleyin
        const transactionSuccess = document.querySelector('div.sc-bczRLJ.gHGHPk > div > div.sc-hKMtZM.sc-iqcoie.vhlUB.ehOBsB');
        if (transactionSuccess) {
            // İşlem başarıyla tamamlandığında döngüyü baştan başlatın
            continue;
        }

        // İşlemi başarıyla tamamlandığında döngüyü baştan başlatın
        await bekle(3000); // Sayfanın yüklenmesini bekleyin (gerektiğinde süreyi ayarlayın)
    }
}

// Ana işlemi başlat
anaIslem();
```


### Şimdi diğer arkadaşlarımızın Rollapp Ağlarını da cüzdanlarımıza ekleyelim, Ne kadar çok rollappta işlem yaparsak hepimiz için iyi olacaktır, (100 Adet Rollapp ağını ekleyelim)

<a href="https://portal.dymension.xyz/rollapp/rues_2215298-1" target="_blank">.1 Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/aazifiri_7919697-1" target="_blank">.1 Enzifiri</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/wwanyone_7167961-1" target="_blank">.2 WWAnyone</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/vevivo_7131032-1" target="_blank">.3 Vevivo</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mutu_2624378-1" target="_blank">.4 Mutu</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/asdas_1155050-1" target="_blank">.5 Asdas</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mert_7750534-1" target="_blank">.6 Mert</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/geralt_7601687-1" target="_blank">.7 Geralt</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/ecamli_5793626-1" target="_blank">.8 Ecamli</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/redwhite_8277135-1" target="_blank">.9 Red White</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/sezarasrollup_6248924-1" target="_blank">.10 Sezaras Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mymucaorollapp_9625159-1" target="_blank">.11 My Mucao Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/khaldrogo_1077576-1" target="_blank">.12 Khaldrogo</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/kananrollapp_3503398-1" target="_blank">.13 Kanan Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/komadorollapp_1761-21" target="_blank">.14 Komado Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/django_5053643-1" target="_blank">.15 Django</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/pavlov_5091355-1" target="_blank">.16 Pavlov</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/bakkalgazi_5148467-1" target="_blank">.17 Bakkalgazi</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/crbaa_2059617-1" target="_blank">.18 Crbaa</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myrollerapp_4555277-1" target="_blank">.19 My Rollerapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/testnetnodes_6811501-1" target="_blank">.20 Testnet Nodes</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/cmdexe_7182178-1" target="_blank">.21 Cmdexe</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/devil_9934124-1" target="_blank">.23 Devil</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/zeycan_3437501-1" target="_blank">.24 Zeycan</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/machvi_3010884-1" target="_blank">.25 Machvi</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myfennarirollapp_9412493-1" target="_blank">.26 My Fennari Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/nuribarturollapp_5906-1" target="_blank">.27 Nuribartu Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/byfalib_6334-1" target="_blank">.28 Byfalib</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/salomonrollapp_3213-1" target="_blank">.29 Salomon Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/sestotestnetrollapp_1188904-1" target="_blank">.30 Sesto Testnet Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/allaboutme_3227000-1" target="_blank">.31 All About Me</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/kingsharald_6676734-1" target="_blank">.32 King Sharald</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/wasowskyrollapp_5241-1" target="_blank">.33 Wasowsky Rollup</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/knowledge_5654358-1" target="_blank">.34 Knowledge</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/svserden_6184578-1" target="_blank">.36 Svserden</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/karahan_5225752-1" target="_blank">.37 Karahan</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/canduesed_7042481-1" target="_blank">.38 Canduesed</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/ckaarraapp_5833550-1" target="_blank">.39 Ckaarraapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/glmsr_2383808-1" target="_blank">.41 Glmsr</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/marilyn_5525101-1" target="_blank">.42 Marilyn</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/bootstraprollapp_9294242-1" target="_blank">.43 Bootstrap Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/aykut_6305294-1" target="_blank">.44 Aykut</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myyasarollapp_6293399-1" target="_blank">.45 My Yasar Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/rodruquez_9822312-1" target="_blank">.46 Rodruquez</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/sicardii_1748361-1" target="_blank">.47 Sicardii</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/asht_2446192-1" target="_blank">.48 Asht</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/fiseq_5929539-1" target="_blank">.49 Fiseq</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/lavenil_9813763-1" target="_blank">.50 Lavenil</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/hakand_1902122-1" target="_blank">.51 Hakand</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/nuribartu_2743708-1" target="_blank">.52 Nuribartu</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/ahmkah_5047738-1" target="_blank">.53 Ahmkah</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/toexecution_2015378-1" target="_blank">.54 To Execution</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myrollenes_8374670-1" target="_blank">.55 My Rollenes</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/eltaz_8782887-1" target="_blank">.57 Eltaz</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/rufath_6047975-1" target="_blank">.58 Rufath</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/karamustafa_5568016-1" target="_blank">.59 Karamustafa</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/kaikisen_2019592-1" target="_blank">.60 Kaikisen</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/gokean_4997912-1" target="_blank">.61 Gokean</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/zionalc_7541620-1" target="_blank">.62 Zionalc</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/gkrollapp_4731583-1" target="_blank">.63 Gkrollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/ysanodes_1145057-1" target="_blank">.64 Ysa Nodes</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/yalper_2816827-1" target="_blank">.65 Yalper</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/kriptosekici_7874642-1" target="_blank">.66 Kriptosekici</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mfttt_6313983-1" target="_blank">.67 Mfttt</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/yanks_4824450-1" target="_blank">.68 Yanks</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mehmetxh_5708076-1" target="_blank">.69 Mehmetxh</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/clixalink_6097386-1" target="_blank">.70 Clixalink</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/kazan_1582447-1" target="_blank">.71 Kazan</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/cagatayyurollapp_8221102-1" target="_blank">.72 Cagatayyu Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/cancan_6930584-1" target="_blank">.73 Cancan</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/mytestnetrunrollapp_33368-1" target="_blank">.74 My Testnet Run Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/aeithalides_3185614-1" target="_blank">.75 Aeithalides</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/llal_2493498-1" target="_blank">.76 Llal</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myser_1494209-1" target="_blank">.77 Myser</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/tskn_9830131-1" target="_blank">.78 Tskn</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/seffa_9700646-1" target="_blank">.79 Seffa</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/nodder_8357480-1" target="_blank">.80 Nodder</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/myfatihsrollapp_7853251-1" target="_blank">.81 My Fatihs Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/erda_3442089-1" target="_blank">.82 Erda</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/emir_9891216-1" target="_blank">.83 Emir</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/ezraikerollapp_6297073-1" target="_blank">.84 Ezraikerollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/nodesruns_5948385-1" target="_blank">.85 Nodesruns</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/arusluk_1613976-1" target="_blank">.86 Arusluk</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/eftay_9825216-1" target="_blank">.87 Eftay</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/utkububa_6461015-1" target="_blank">.88 Utkububa</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/zozak_8767363-1" target="_blank">.89 Zozak</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/taurusrollapp_2484522-1" target="_blank">.92 Taurus Rollapp</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/burcukale_4112966-1" target="_blank">.93 Burcukale</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/sacitt_3701850-1" target="_blank">.94 Sacitt</a>  <br>
<a href="https://portal.dymension.xyz/rollapp/arusluk_1613976-1" target="_blank">.95 Arusluk</a>  <br>
 
