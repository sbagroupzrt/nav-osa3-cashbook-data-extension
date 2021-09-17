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

### Számla szintű megjegyzés

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a számla megjegyzése. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00001_INVOICE_COMMENT</dataName>
        <dataDescription>Invoice comment</dataDescription>
        <dataValue>                    
            Tárhely számla.
        </dataValue>
    </additionalInvoiceData>
    ...
</invoiceData>
...
```
### Számla szintű munkaszám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a számlához tartozó munkaszám. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00002_WORK_NUMBER</dataName>
        <dataDescription>Invoice work number</dataDescription>
        <dataValue>                    
            AWS
        </dataValue>
    </additionalInvoiceData>
    ...
</invoiceData>
...
```
### Számla szintű nettó főkönyvi szám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a számlához tartozó nettó főkönyvi szám. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00003_LEDGER_NETTO</dataName>
        <dataDescription>Ledger number for invoice netto</dataDescription>
        <dataValue>                    
            911
        </dataValue>
    </additionalInvoiceData>
    ...
</invoiceData>
...
```
### Számla szintű áfa főkönyvi szám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a számlához tartozó áfa főkönyvi szám. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00004_LEDGER_TAX</dataName>
        <dataDescription>Ledger number for invoice tax</dataDescription>
        <dataValue>                    
            467
        </dataValue>
    </additionalInvoiceData>
    ....
</invoiceData>
...
```
### Számla szintű bruttó főkönyvi szám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a számlához tartozó bruttó főkönyvi szám. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00005_LEDGER_GROSS</dataName>
        <dataDescription>Ledgern number for invoice gross</dataDescription>
        <dataValue>                    
            311
        </dataValue>
    </additionalInvoiceData>
    ...
</invoiceData>
...
```
### Tétel szintű nettó főkönyvi szám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó nettó főkönyvi szám. Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00006_LEDGER_NETTO</dataName>
        <dataDescription>Ledger number for line netto</dataDescription>
        <dataValue>                    
            911
        </dataValue>
    </additionalLineData>
    ...
</line>
...
```
### Tétel szintű áfa főkönyvi szám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó áfa főkönyvi szám. Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00007_LEDGER_TAX</dataName>
        <dataDescription>Ledger number for line tax</dataDescription>
        <dataValue>                    
            467
        </dataValue>
    </additionalLineData>
    ....
</line>
...
```
### Tétel szintű fökönyvi elnevezés

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó főkönyvi elnevezés (pl.: anyagköltség, áramdíj, értékesítés árbevétel). Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00008_LEDGER_TITLE</dataName>
        <dataDescription>Ledger title</dataDescription>
        <dataValue>                    
            Értékesítés árbevétel
        </dataValue>
    </additionalLineData>
    ....
</line>
...
```
### Tétel szintű áfa bevaállsi sor

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó áfa bevallási sor. Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00009_VAT_RETURN_LINE</dataName>
        <dataDescription>Vat return line</dataDescription>
        <dataValue>                    
            06
        </dataValue>
    </additionalLineData>
    ....
</line>
...
```
### Tétel szintű munkaszám

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó munkaszám. Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00011_WORK_NUMBER</dataName>
        <dataDescription>Work number for line</dataDescription>
        <dataValue>                    
            MSZ-22522
        </dataValue>
    </additionalLineData>
    ....
</line>
...
```
### Tétel szintű megjegyzés

Van lehetőség arra, hogy az XML fájlban átadásra kerüljön a tételhez tartozó megjegyzés. Ehhez az OSA3 XSD álltál definiált **additionalLineData** elemet kell alkalmazni az alábbiak szerint.
```
...
<line>
    ...
    <additionalLineData>
        <dataName>C00012_COMMENT</dataName>
        <dataDescription>Comment for line</dataDescription>
        <dataValue>                    
            Futár
        </dataValue>
    </additionalLineData>
    ....
</line>
...
```

## Szállító számlák

Ha az integrálásra kerülő program tart nyilván szállító számlákat, akkor van lehetőség azokat isfeladni a Cashbook-nak. Ehhez azt kell tenni, hogy a szállító számlák adataiból is kell generálni egy XML-t, ahol a vevő lesz az a vállalkozás, aki befogadta a számlákat, valamint ki kell egészíteni egy **additionalInvoiceData** elemmel, ami megmondja a Cashbook-nak, hogyz szállító számla.

Ha ez az elem hiányzik, akkor a Cashbook alapból vevő számlának tekinti a beérkező adatokat, ha az elem megtalálható, akkor a tartalma lehet income (bevétel, azaz vevő számla) vagy expense(kiadás, azaz szállító számla).
```
...
<invoiceData>
    ...
    <additionalInvoiceData>
        <dataName>C00010_INVOICE_TYPE</dataName>
        <dataDescription>Invoice is an expense or an income</dataDescription>
        <dataValue>                    
            expense
        </dataValue>
    </additionalInvoiceData>
    ...
</invoiceData>
...
```

## Kiegyenlítés

A kibővített adatszerkezettel van lehetőség a kiegyenlítések adatainak átadására, amita Cashbook továbbít a könyvelőprogram felé. Amennyiben a számla kibocsájtása után újabb kiegyenlítést tud az Ügyfél rögzíteni a számlázó programban, abban az esetben az egész XML újra küldhető (az új és régi kiegyenlítésekkel együtt) és a kiegyenlítés bekerül a pénzügyi tétel adatai közé. A további kiegyenlítések beküldése esetén a PDF számlakép nem szükséges, azonban a POST mezőt el kell küldeni a payments tartalommal.
```
...
<invoice>
    ...
    <invoicePayments>
        <payment>
            <locationCode>P</locationCode>
            <locationLedger>3811</locationLedger>
            <paymentMethod>CASH</paymentMethod>
            <paymentDate>2019-08-01</paymentDate>
            <amount>55000</amount>
            <currencyCode>HUF</currencyCode>
            <exchangeRate>1</exchangeRate>
            <warrantNumber>PB-201908-21558</warrantNumber>
            <paymentComment>Pénztárba befizette.</paymentComment>
        </payment>
    </invoicePayments>
</invoice>
...
```
A kiegyenlítés helye: P -> Pénztár, B -> Bank, fizetési mód következő pontban részletezve.

## A sémától eltérő fizetési módok

Lehetőségünk van az XML fájlban az XSD alapértelmezett fizetési módjaihoz képest (CASH, TRANSFER, CARD, VOUCHER, OTHER) további fizetési módokat megadni. A további fizetési módok átadásához szükséges, hogy a paymentMethod értéke OTHER legyen és tartalmazza az XML az alábbi additionalInvoiceData-t:
```
...
<invoiceData>
    ...
    <paymentMethod>OTHER</paymentMethod>
    ...
    <additionalInvoiceData>
      <dataName>C00013_ADDITIONAL_PAYMENT_METHOD</dataName>
      <dataDescription>Additional payment methods</dataDescription>
      <dataValue>COLLECTION</dataValue>
    </additionalInvoiceData>
    ....
</invoiceData>
...
```

A dataValue mező értékei a következők lehetnek:

* CHECK: csekkes fizetési mód
* ENCASHMENT: inkasszó
* COMPENZATION: kompenzáció
* CASHONDELIVERY: utánvét
* COLLECTION: csoportos beszedés

## Számlakép (PDF)

A számlához tartozó számlakép beküldhető az XML részekként BASE64 kódolt szövegben. Ehhez az OSA3 XSD álltál definiált **additionalInvoiceData** elemet kell alkalmazni az alábbiak szerint.
```
...
<additionalInvoiceData>
    <dataName>C00000_BASE64_PDF</dataName>
    <dataDescription>PDF</dataDescription>
    <dataValue>Ide jön a PDF fájl tartalma BASE64-ben</dataValue>
</additionalInvoiceData>
...
```

## Impresszum

SBA Group Zrt.  
1108 Budapest, Bányató utca 13.  
MineLake irodaház  
25566552-2-42  
E-mail: info@cashbook.hu  
Telefonszám: +36 1/998-8506 (munkanapokon 10:00-16:00 óra között)
