# E kūkulu i kāu kikowaena hoʻouna leka uila SMTP

## olelo mua

Hiki iā SMTP ke kūʻai pololei i nā lawelawe mai nā mea kūʻai kapua, e like me:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali kapua leka uila](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Hiki iā ʻoe ke kūkulu i kāu kikowaena leka uila - hoʻouna palena ʻole, haʻahaʻa haʻahaʻa.

Ma lalo, hōʻike mākou i kēlā me kēia pae pehea e kūkulu ai i kā mākou kikowaena leka uila.

## Koho kikowaena

Pono ka server SMTP hoʻokipa ponoʻī i IP ākea me nā awa 25, 456, a me 587 wehe.

Ua ālai ʻia kēia mau awa ma ke ʻano maʻamau o nā ao lehulehu, a hiki ke wehe ʻia ma ka hoʻopuka ʻana i kahi kauoha hana, akā pilikia loa ia ma hope.

Manaʻo wau e kūʻai mai kahi pūʻali i wehe ʻia kēia mau awa a kākoʻo i ka hoʻonohonoho ʻana i nā inoa inoa hoʻohuli.

Eia, paipai wau [iā Contabo](https://contabo.com) .

ʻO Contabo kahi mea hoʻolako kikowaena e hoʻokumu ʻia ma Munich, Kelemānia, i hoʻokumu ʻia ma 2003 me nā kumukūʻai hoʻokūkū loa.

Inā koho ʻoe i ka Euro ma ke kālā o ke kūʻai ʻana, e ʻoi aku ka liʻiliʻi o ke kumukūʻai (kahi kikowaena me 8GB hoʻomanaʻo a me 4 CPUs e pili ana i 529 yuan i kēlā me kēia makahiki, a ʻo ka uku hoʻonohonoho mua ʻana no hoʻokahi makahiki).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Ke kau ʻana i kahi kauoha, `prefer AMD` , a ʻoi aku ka maikaʻi o ka hana o ka server me AMD CPU.

Ma lalo iho nei, e lawe au i ka VPS o Contabo i laʻana e hōʻike ai pehea e kūkulu ai i kāu kikowaena leka uila.

## hoʻonohonoho ʻōnaehana ʻo Ubuntu

ʻO ka ʻōnaehana hana ma aneʻi ʻo Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Inā hōʻike ke kikowaena ma ssh `Welcome to TinyCore 13!` (e like me ka mea i hōʻike ʻia ma ke kiʻi ma lalo), ʻo ia ka mea ʻaʻole i hoʻokomo ʻia ka ʻōnaehana. E ʻoluʻolu e wehe i ka ssh a kali no kekahi mau minuke e komo hou.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ke hōʻike ʻia `Welcome to Ubuntu 22.04.1 LTS` , ua pau ka hoʻomaka ʻana, a hiki iā ʻoe ke hoʻomau i kēia mau ʻanuʻu.

### [Koho] E hoʻomaka i ke kaiapuni hoʻomohala

He koho kēia ʻanuʻu.

No ka maʻalahi, kau wau i ka hoʻonohonoho ʻana a me ka hoʻonohonoho ʻōnaehana o ka polokalamu ubuntu ma [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

E holo i kēia kauoha e hoʻouka me hoʻokahi kaomi.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

ʻO nā mea hoʻohana Pākē, e ʻoluʻolu e hoʻohana i kēia kauoha ma kahi, a e hoʻonohonoho ʻia ka ʻōlelo, ka palena manawa, a pēlā aku.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Hiki iā Contabo iā IPV6

E ho'ā i ka IPV6 i hiki iā SMTP ke hoʻouna i nā leka uila me nā helu IPV6.

hoʻoponopono `/etc/sysctl.conf`

Hoʻololi a hoʻohui paha i kēia mau laina

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

E hahai me [ke aʻo contabo: Hoʻohui i ka pilina IPv6 i kāu kikowaena](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Hoʻoponopono `/etc/netplan/01-netcfg.yaml` , hoʻohui i kekahi mau laina e like me ka mea i hōʻike ʻia ma ke kiʻi ma lalo nei (Contabo VPS default configuration file ua loaʻa kēia mau laina, e wehe wale iā lākou).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

A laila `netplan apply` e hoʻokō i ka hoʻonohonoho hoʻololi ʻia.

Ma hope o ka holomua o ka hoʻonohonoho ʻana, hiki iā ʻoe ke hoʻohana i `curl 6.ipw.cn` e nānā i ka helu IPv6 o kāu pūnaewele waho.

## Hoʻopili i nā hana waihona hoʻonohonoho

```
git clone https://github.com/wactax/ops.soft.git
```

## E hana i kahi palapala SSL manuahi no kou inoa inoa

Pono ka hoʻouna ʻana i ka leka uila i kahi palapala SSL no ka hoʻopili ʻana a me ke kau inoa ʻana.

Hoʻohana mākou i [ka acme.sh](https://github.com/acmesh-official/acme.sh) e hana i nā palapala hōʻoia.

ʻO acme.sh kahi mea hana hoʻopaʻa inoa ʻokoʻa i wehe ʻia,

E hoʻokomo i ka hale waihona hoʻonohonoho ops.soft, holo `./ssl.sh` , a e hana ʻia kahi waihona `conf` ma **ka papa kuhikuhi luna** .

E huli i kāu mea hoʻolako DNS mai [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , hoʻoponopono `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

A laila e holo i `./ssl.sh 123.com` e hana i nā palapala hōʻoia `123.com` a me `*.123.com` no kou inoa inoa.

ʻO ka holo mua e hoʻokomo i [ka acme.sh](https://github.com/acmesh-official/acme.sh) a hoʻohui i kahi hana i hoʻonohonoho ʻia no ka hoʻohou hou. Hiki iā ʻoe ke ʻike `crontab -l` , aia kahi laina penei.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

ʻO ke ala no ka palapala hōʻoia e like me `/mnt/www/.acme.sh/123.com_ecc。`

E kāhea ka palapala hōʻoia `conf/reload/123.com.sh` script, hoʻoponopono i kēia palapala, hiki iā ʻoe ke hoʻohui i nā kauoha e like me ka `nginx -s reload` e hōʻoluʻolu i ka cache palapala o nā noi pili.

## E kūkulu i kahi kikowaena SMTP me ka chasquid

ʻO [chasquid](https://github.com/albertito/chasquid) kahi kikowaena SMTP kumu wehe i kākau ʻia ma ka ʻōlelo Go.

Ma ke ʻano he pani no nā polokalamu kikowaena leka kahiko e like me Postfix a me Sendmail, ʻoi aku ka maʻalahi o ka chasquid a maʻalahi hoʻi e hoʻohana, a ʻoi aku ka maʻalahi no ka hoʻomohala kiʻekiʻe.

Holo `./chasquid/init.sh 123.com` e hoʻokomo ʻokoʻa me hoʻokahi kaomi (e hoʻololi iā 123.com me kāu inoa kikowaena hoʻouna).

## E hoʻonohonoho i ka pūlima leka uila DKIM

Hoʻohana ʻia ʻo DKIM e hoʻouna i nā pūlima leka uila e pale i nā leka mai ka mālama ʻia ʻana ma ke ʻano he spam.

Ma hope o ka holo pono ʻana o ke kauoha, e koi ʻia ʻoe e hoʻonohonoho i ka moʻolelo DKIM (e like me ka hōʻike ʻana ma lalo nei).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Hoʻohui wale i kahi moʻolelo TXT i kāu DNS (e like me ka mea i hōʻike ʻia ma lalo nei).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Nānā i ke kūlana lawelawe a me nā moʻolelo

 `systemctl status chasquid` Nānā i ke kūlana lawelawe.

ʻO ke kūlana o ka hana maʻamau e like me ka mea i hōʻikeʻia ma ke kiʻi ma lalo nei

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` a i ʻole `journalctl -xeu chasquid` ke nānā i ka log hala.

## Hoʻololi i ka hoʻonohonoho inoa ʻāina

ʻO ka inoa inoa hope e ʻae i ka helu IP e hoʻoholo i ka inoa kikowaena pili.

ʻO ka hoʻonohonoho ʻana i kahi inoa inoa hope hiki ke pale i nā leka uila mai ka ʻike ʻia ʻana he spam.

I ka loaʻa ʻana o ka leka uila, e hoʻokō ka server e loaʻa ana i ka nānā ʻana i ka inoa o ka inoa inoa ma ka IP address o ka mea hoʻouna hoʻouna e hōʻoia inā loaʻa i ka mea hoʻouna hoʻouna ka inoa inoa hope.

Inā ʻaʻole i loaʻa i ka mea hoʻouna ka inoa inoa hope a inā ʻaʻole i kūlike ka inoa inoa hope i ka IP address o ke kikowaena hoʻouna, hiki i ka mea hoʻouna ke hoʻomaopopo i ka leka uila he spam a hōʻole paha.

E kipa [https://my.contabo.com/rdns](https://my.contabo.com/rdns) a hoʻonohonoho e like me ka hōʻike ʻana ma lalo nei

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Ma hope o ka hoʻonohonoho ʻana i ka inoa inoa hope, e hoʻomanaʻo e hoʻonohonoho i ka hoʻonā mua o ka inoa domain ipv4 a me ipv6 i ke kikowaena.

## Hoʻoponopono i ka inoa hoʻokipa o chasquid.conf

Hoʻololi i `conf/chasquid/chasquid.conf` i ka waiwai o ka inoa ʻaoʻao hope.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

A laila e holo i `systemctl restart chasquid` e hoʻomaka hou i ka lawelawe.

## Hoʻihoʻi i ka conf i ka waihona git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

No ka laʻana, hoʻihoʻi au i ka waihona conf i kaʻu kaʻina hana github penei

E hana mua i kahi hale kūʻai pilikino

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

E hoʻokomo i ka papa kuhikuhi conf a waiho i ka hale kūʻai

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Hoʻohui i ka mea hoʻouna

holo

```
chasquid-util user-add i@wac.tax
```

Hiki ke hoʻohui i ka mea hoʻouna

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### E hōʻoia ua hoʻonohonoho pono ʻia ka ʻōlelo huna

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Ma hope o ka hoʻohui ʻana i ka mea hoʻohana, `chasquid/domains/wac.tax/users` e hōʻano hou ʻia, e hoʻomanaʻo e waiho i ka hale kūʻai.

## DNS hoʻohui SPF moʻolelo

ʻO SPF (Sender Policy Framework) kahi ʻenehana hōʻoia leka uila i hoʻohana ʻia e pale i ka hoʻopunipuni leka uila.

Hōʻoia ʻo ia i ka ʻike o ka mea hoʻouna leka ma ka nānā ʻana i ka helu IP o ka mea hoʻouna i pili me nā moʻolelo DNS o ka inoa domain i ʻōlelo ʻia, e pale ana i nā mea hoʻopunipuni mai ka hoʻouna ʻana i nā leka uila hoʻopunipuni.

ʻO ka hoʻohui ʻana i nā moʻolelo SPF hiki ke pale i nā leka uila mai ka ʻike ʻia ʻana he spam e like me ka hiki.

Inā ʻaʻole kākoʻo kāu kikowaena inoa kikowaena i ke ʻano SPF, e hoʻohui wale i ka moʻolelo ʻano TXT.

No ka laʻana, penei ka SPF o `wac.tax`

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF no `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

E hoʻomaopopo ua `include:_spf.google.com` ma aneʻi, no ka mea e hoʻonohonoho wau `i@wac.tax` ma ke ʻano he helu hoʻouna ma ka pahu leta Google ma hope.

## Hoʻonohonoho DNS DMARC

ʻO DMARC ka pōkole o (Domain-based Message Authentication, Reporting & Conformance).

Hoʻohana ʻia ia no ka hopu ʻana i nā bounce SPF (ma muli paha o nā hewa o ka hoʻonohonoho ʻana, a i ʻole e hoʻohua nei kekahi e hoʻouna i ka spam).

Hoʻohui i ka moʻolelo TXT `_dmarc` ,

Penei ka ʻike

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

ʻO ke ʻano o kēlā me kēia ʻāpana penei

### p (Kulekele)

Hōʻike i ke ʻano o ka mālama ʻana i nā leka uila i hāʻule ʻole i ka hōʻoia SPF (Sender Policy Framework) a i ʻole DKIM (DomainKeys Identified Mail). Hiki ke hoʻonohonoho ʻia ka ʻāpana p i kekahi o nā waiwai ʻekolu:

* ʻaʻohe: ʻAʻohe hana i hana ʻia, ʻo ka hopena hōʻoia wale nō e hānai ʻia i ka mea hoʻouna ma o ka leka uila hōʻike.
* Quarantine: E kau i ka leka i hala ʻole i ka hōʻoia i loko o ka waihona spam, akā ʻaʻole e hōʻole pololei i ka leka uila.
* hōʻole: hōʻole pololei i nā leka uila i hāʻule i ka hōʻoia.

### fo (Nā koho hāʻule)

Hōʻike i ka nui o ka ʻike i hoʻihoʻi ʻia e ka mīkini hōʻike. Hiki ke hoʻonohonoho ʻia i kekahi o kēia mau waiwai:

* 0: E hōʻike i nā hopena hōʻoia no nā memo āpau
* 1: E hōʻike wale i nā memo i hāʻule i ka hōʻoia
* d: E hōʻike wale i nā hemahema o ka hōʻoia inoa ʻāina
* s: hōʻike wale i nā hemahema hōʻoia SPF
* l: Hōʻike wale i nā hemahema hōʻoia DKIM

### rua & ruf

* rua (Hōʻike URI no nā hōʻike Hui Pū ʻIa): He leka uila no ka loaʻa ʻana o nā hōʻike hōʻuluʻulu
* ruf (Hōʻike URI no nā hōʻike Forensic): leka uila e loaʻa i nā hōʻike kikoʻī

## Hoʻohui i nā moʻolelo MX no ka hoʻouna ʻana i nā leka uila iā Google Mail

No ka mea, ʻaʻole hiki iaʻu ke loaʻa kahi pahu leta hui manuahi e kākoʻo ana i nā helu wahi āpau (Catch-All, hiki ke loaʻa i nā leka uila i hoʻouna ʻia i kēia inoa domain, me ka ʻole o ke kaohi ʻana i nā prefixes), ua hoʻohana au i ka chasquid e hoʻouna i nā leka uila āpau i kaʻu pahu leta Gmail.

**Inā loaʻa iā ʻoe kāu pahu leka pāʻoihana uku ponoʻī, mai hoʻololi i ka MX a lele i kēia kaʻina.**

Hoʻoponopono `conf/chasquid/domains/wac.tax/aliases` , hoʻonohonoho i ka pahu leta hoʻouna

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` hōʻike i nā leka uila a pau, ʻo `i` ka prefix leka uila o ka mea hoʻouna i hana ʻia ma luna. No ka hoʻouna ʻana i ka leka uila, pono kēlā me kēia mea hoʻohana e hoʻohui i kahi laina.

A laila e hoʻohui i ka moʻolelo MX (kuhikuhi pololei wau i ka helu wahi o ka inoa inoa hope ma aneʻi, e like me ka mea i hōʻike ʻia ma ka laina mua o ke kiʻi ma lalo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Ma hope o ka pau ʻana o ka hoʻonohonoho ʻana, hiki iā ʻoe ke hoʻohana i nā leka uila ʻē aʻe e hoʻouna i nā leka uila iā `i@wac.tax` a me `any123@wac.tax` e ʻike inā hiki iā ʻoe ke loaʻa nā leka uila ma Gmail.

Inā ʻaʻole, e nānā i ka log chasquid ( `grep chasquid /var/log/syslog` ).

## E hoʻouna i leka uila iā i@wac.tax me Google Mail

Ma hope o ka loaʻa ʻana o ka leka uila iā Google Mail, manaʻo maoli wau e pane me `i@wac.tax` ma kahi o i.wac.tax@gmail.com.

E kipa [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) a kaomi iā "Add another email address".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

A laila, e hoʻokomo i ke code hōʻoia i loaʻa e ka leka uila i hoʻouna ʻia iā.

ʻO ka hope, hiki ke hoʻonohonoho ʻia ma ke ʻano he helu hoʻouna paʻamau (me ke koho e pane me ka helu like).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ma kēiaʻano, ua hoʻopau mākou i ka hoʻokumuʻana i ke kikowaena leka uila SMTP a ma ka manawa like e hoʻohana i ka Google Mail e hoʻouna a loaʻa i nā leka uila.

## E hoʻouna i leka uila hoʻāʻo e nānā inā ua holomua ka hoʻonohonoho

E komo i ka `ops/chasquid`

E holo i `direnv allow` e hoʻokomo i nā hilinaʻi (ua hoʻokomo ʻia ʻo direnv i ke kaʻina hana hoʻomaka hoʻokahi kī mua a ua hoʻohui ʻia kahi makau i ka pūpū)

alaila holo

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Penei ke ano o na palena

* mea hoʻohana: SMTP mea hoʻohana
* hele: SMTP password
* i: ka mea loaa

Hiki iā ʻoe ke hoʻouna i leka uila hoʻāʻo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Manaʻo ʻia e hoʻohana iā Gmail no ka loaʻa ʻana o nā leka uila hoʻāʻo e nānā inā kūleʻa nā hoʻonohonoho.

### TLS hoʻopunipuni maʻamau

E like me ka mea i hōʻike ʻia ma ke kiʻi ma lalo nei, aia kēia laka liʻiliʻi, ʻo ia hoʻi ua hoʻokō pono ʻia ka palapala SSL.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

A laila kaomi "Show Original Email"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

E like me ka mea i hōʻike ʻia ma ke kiʻi ma lalo nei, hōʻike ka ʻaoʻao leka uila Gmail iā DKIM, ʻo ia hoʻi ua kūleʻa ka hoʻonohonoho DKIM.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

E nānā i ka Loaʻa ma ke poʻo o ka leka uila mua, a hiki iā ʻoe ke ʻike i ka helu o ka mea hoʻouna ʻo IPV6, ʻo ia hoʻi ua hoʻonohonoho pono ʻia ʻo IPV6.
