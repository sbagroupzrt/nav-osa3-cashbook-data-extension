![Cashbook](https://cashbook.hu/site/img/cashbook-logo@3x.png)
## NAV OSA3 XML Cashbook adatbővítés

Az OSA3 XML adatbővítés azzal a céllal készült, hogy a kötelező adatszolgáltatással nem érintett adatok és számlák adati, valamint további számviteli értelemben értékes adatok könnyedén eljuthassanak a számlázó programokból, ügyviteli rendszerekből a könyvelő programokba a Cashbook-kon keresztül.

A kibővített XML érvényes XML, de az OSA3 XSD-jével nem validálható. Terveink között szerepel átdolgozni úgy, hogy XSD valid maradjon, de mivel indulás óta tökéltesen működik és ez senkinél nem jelentett problémát, egyelőre nem prioritás.

![Cashbook](https://cashbook.hu/site/img/illustration_02_whitebg_render.gif)

Jelenleg ezek a számlázó programok használják a kibővített adatstruktúrát és adnak át adatot a Cashbbook-ba (ABC sorrendben):

* Billingo
* Canon Therefore
* DREAM4SYS
* In-Cash
* Kulcs Üzlet
* Naturasoft
* RLB

## Az adatbővítés ajánlott alkalmazása

### Bevált módszer adatszolgáltatás alá eső számlák esetében

A számlázó program az előírásoknak megfelelően elkészíti az OSA3 XML-t és teljesíti az adatszolgáltatást, majd kiegészíti az XML-t a további adatokkal és azt hasonló módszerrel elküldi a Cashbook API-nak.

### Bevált módszer adatszolgáltatás alá nem eső számlák esetében

A számlázó program létrehoz egy olyan XML állományt, amiben minden lehetséges adat megtalálható ahhoz, hogy a könyvelőprogramban pénzügyi tétel lehessen belőle és alkalmas legyen a könyvelésre és azt hasonló módszerrel elküldi a Cashbook API-nak.

## A bővítéssel nem érintett, de figyelmet igénylő adatok

Vannak esetek, amikor az OSA3 XML kibővítés olyan adatokat érint, ami egyébként nem az adatbővítés része. Ez tipikusan a magánszemélyes vevők számlái, amikor is a NAV-hoz nem kerül beküldésre a vevő neve és címe.

A módszer ugyan az, mint az előzőekben említett, azonban ebben az esetben az adatszolgáltatás után az OSA3 XSD-je szerinti megfelelő mezők kerülnek feltöltésre. Ezt követően az XML ugyan úgy elküldésre kerül a Cashbook API-jánk.

## A bővített adatok

* Kiegyenlítés
* Számla szintű megjegyzés
* Számla szintű munkaszám
* Számla szintű nettó főkönyvi szám
* Számla szintű áfa főkönyvi szám
* Számla szintű bruttó főkönyvi szám
* Tétel szintű nettó főkönyvi szám
* Tétel szintű áfa főkönyvi szám
* Tétel szintű bruttó főkönyvi szám
* Tétel szintű áfa bevaállsi sor
* Tétel szintű elnevezés (WIP)

## Szállító számlák

Ha az integrálásra kerülő program tart nyilván szállító számlákat, akkor van lehetőség azokat isfeladni a Cashbook-nak. Ehhez azt kell tenni, hogy a szállító számlák adataiból is kell generálni egyXML-t, ahol a vevő lesz az a vállalkozás, aki befogadta a számlákat, valamint ki kell egészíteni egyadditionalInvoiceData elemmel (C00010_INVOICE_TYPE), ami megmondja a Cashbook-nak, hogyaz szállító számla.

Ha ez az elem hiányzik, akkor a Cashbook alapból vevő számlának tekinti a beérkező adatokat, haaz elem megtalálható, akkor a tartalma lehet income (bevétel, azaz vevő számla) vagy expense(kiadás, azaz szállító számla).

## Kiegyenlítések

Amennyiben a számla kibocsájtása után újabb kiegyenlítést tud az Ügyfél rögzíteni a számlázó programban, abban az esetben az egész XML újra küldhető (az új és régi kiegyenlítésekkel együtt) és a kiegyenlítés bekerül a pénzügyi tétel adatai közé. A további kiegyenlítések beküldése esetén a PDF számlakép nem szükséges, azonban a POST mezőt el kell küldeni a payments tartalommal.

## Számlakép (PDF)
