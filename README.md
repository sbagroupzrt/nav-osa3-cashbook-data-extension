## NAV OSA3 XML Cashbook adatkibővítés

![Cashbook](https://kreativ-informatika.cashbook.hu/site/anim/anim_01_.mp4)

Az OSA3 XML adatkibővítés azzal a céllal készült, hogy a kötelező adatszolgáltatással nem érintett adatok és számlák adati, valamint további számviteli értelemben értékes adatok könnyedén eljuthassanak a számlázó programokbból, ügyviteli rendszerekből a könyvelő programokba a Cashbook-kon keresztül.

Jelenleg ezek a számlázó programok használják a kibővített adatstruktúrát és adnak át adatot a Cashbbook-ba (ABC sorrendben):

* Billingo
* Canon Therefore
* DREAM4SYS
* In-Cash
* Kulcs Üzlet
* Naturasoft
* RLB

## Az adatkibővítés ajánlott alkalmazása

### Bevált módszer adatszolgáltatás alá eső számlák esetébben

A számlázó program az előírásoknak megfelelően elkészíti az OSA3 XML-t és teljesíti az adatszolgáltatást, majd kieggészíti az XML-t a további adatokkal és azt hasonló módszerrel elküldi a Cashbbook API-jának.

### Bevált módszer adatszolgáltatás alá nem eső számlák esetébben

A számlázó program létrehoz egy olyan XML állományt, amiben minden lehetséegs adat megtalálható ahhoz, hogy a könyvelőprogramban pénzügyi tétel lehessen belőle és alkalmas legyen a könyvelésre és azt hasonló módszerrel elküldi a Cashbbook API-jának.

## A kibővítéssel nem érintett adatok

Vannak esetek, amikor az OSA3 XML kibővítés olyan adatokat érint, ami egyébként nem az adatkibővítés része. Ez tipikusan a magánszemélyes vevők számlái, amikor is a NAV-hoz nem kerül bebküldésre a vevő neve és címe.

A módszer ugyan az, mint az előzőekben említett, azonban ebben az esetben az adatszolgáltatás után az OSA3 XSD-je szerinti megfelelő mezők kerülnek feltöltésre. Ezt követően az XML ugyan úgy elküldésre kerül a Cashbook API-jánk.
