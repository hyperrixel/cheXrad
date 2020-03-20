[![Generic badge](https://img.shields.io/badge/Version-v0.1.0-001850.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/Languages-EN,HU-001850.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/State-Under_development-ffa000.svg)](https://shields.io/)\
[Az angol változatot ide kattintva érheti el.](https://github.com/hyperrixel/cheXrad/blob/master/README.md)

# cheXrad - Pulmonológiai Diagnosztizáló CoCoLo-alapú Program

## A projektről

![logo](chexrad_logo.png)

## A projektről

E projekttel a célunk egy CoCoLo-alapú (Compound of Classification only Looked once: Csak egyszer klasszifikáló) program, amely segíti az orvosoknak a pulmonológiai diagnózis felállításában.

## Munkafolyamat

A program az alábbi módon működik:

- A program megkapja a mellkasi ` PA ` röntgen képet.
- Olyan átalakításokat végez a képen, amelyek a ResNet hálózat használatához szükségesek.
- A kép továbbításra kerül a maghálózatnak, amely egy ResNet architektúra a végső klasszifikáló réteg nélkül.
- A kimeneti adatok továbbítódnak a klasszifikáló hálózatoknak.
- Az eredmény adatláncként kerül megjelenítésre.

## A program specifikációja

### Bemeneti kép

A bemeneti képnek mellkasi röntgen felvételnek kell lennie. A fájl formátuma lehet ` jpeg ` vagy ` png `. A ` DICOM ` formátum támogatása jelenleg fejlesztés alatt áll. A kép mérete nem számít, de a jó eredmény elérése érdekében ajánlott nagyobbnak lennie, mint 224*244. A kép lehetőleg csak ` ROI ` (Region of Interest: fontos terület) területet tartalmazzon, kerülve az üres oldalsó sávokat és a szükségtelen adatokat.

MEGJEGYZÉS: Ne használjon telefonnal vagy kamerával készült képeket, amelyeket képernyőről, monitorról, vagy projektorról rögzített, mert ez negatívan hat a teljesítményre. A modellünk az orvostudományban gyakran használt, átlagos minőségű képeket tartalmazó adatbázisokon volt tanítva és tesztelve.

### Képátalakítás

A program egyik része átalakítja a bemeneti képet a maghálózat igényei alapján. Ez a transzformálás átméretezést és normalizálást jelent.

### Maghálózat

Az átalakított képet először a maghálózat dolgozza fel. Ez általános feldolgozást jelent, amelynek részeként felismerésre kerülnek a képen látható élek, sarokpontok, objektumok és egyéb gyakori tulajdonságok, ismérvek. A maghálózat egy előtanított, de fejetlen, vagyis végső klasszifikáló réteg nélküli ResNet modell. A képfeldolgozásban nagyon gyakori módszer, hogy ilyen modelleket használnak, mert ezek nagyon jól előtanítottak általános és gyakori mintázatokat tartalmazó képeken, így kiválóak a vizuális minták felismerésében.

### A klasszifikáló hálózatok

A feldolgozott adat továbbításra kerül a négy különböző klasszifikáló hálózathoz. Ez a módszer (CoCoLo) jelentős teljesítménynövekedést eredményez, mert a gyakori mintázatokat csak egyszer ismeri fel. A klasszifikáló hálózatokat mi tanítjuk be.

#### Klasszifikáló#1: egészséges - nem egészséges

#### Klasszifikáló#2:

#### Klasszifikáló#3:

#### Klasszifikáló#4:

### Eredmény megjelenítése

A program ezen része a valódi felhasználói interfész (UI). A kinézet részletei attól függnek, hogy éppen milyen platformon fut a rendszer. Ennek ellenére vannak közös tulajdonságaik is.

#### Közös UI karakterisztika

#### Platform specifikus részletek

##### Python szkript

##### Parancssoros applikáció

##### Android applikáció

## A projekt aktuális állása

- [ ] Modul#1 (egészséges, nem egészséges klasszifikáló) betanítás alatt.
- [ ] Modul#2 (2 osztályos klasszifikáló) betanítás alatt.
- [ ] Modul#3 (3 osztályos klasszifikáló) betanítás alatt.
- [ ] Modul#4 (15 osztályos klasszifikáló) betanítás alatt.

## Források és referenciák

### Kép adatbázisok

Az adatbázisok az angol abc szerinti alfabetikus rendben követik egymást és angolul vannak feltüntetve.

#### covid-chestxray-dataset

Published: 2020-02-14\
Contributor(s): [Joseph Paul Cohen: @ieee8023](https://github.com/ieee8023)\
Contact(s): [Joseph Paul Cohen. Postdoctoral Fellow, Mila, University of Montreal](https://josephpcohen.com/)\
Link: [Github repository](https://github.com/ieee8023/covid-chestxray-dataset)\

#### Large Dataset of Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images

Published: 2018-06-01\
Version: 3\
DOI: 10.17632/rscbjbr9sj.3\
Contributor(s): [Daniel Kermany](https://www.mendeley.com/profiles/daniel-kermany2/), Kang Zhang, Michael Goldbaum\
Link: [dataset](https://data.mendeley.com/datasets/rscbjbr9sj/3)\

#### NIH Chest X-ray Dataset of 14 Common Thorax Disease Categories

Published: 2017-09-27 on [NIH official website](https://www.nih.gov/news-events/news-releases/nih-clinical-center-provides-one-largest-publicly-available-chest-x-ray-datasets-scientific-community)\
Contributor(s): [Ronald M. Summers, M.D., Ph.D.](https://www.cc.nih.gov/drd/summers.html)\
Paper: [ChestX-ray8: Hospital-scale Chest X-ray Database and Benchmarks on Weakly-Supervised Classification and Localization of Common Thorax Diseases](http://openaccess.thecvf.com/content_cvpr_2017/papers/Wang_ChestX-ray8_Hospital-Scale_Chest_CVPR_2017_paper.pdf)\
Paper contributor(s): Xiaosong Wang, Yifan Peng, Le Lu, Zhiyong Lu, Mohammadhadi Bagheri, Ronald M. Summers\
Paper contact(s): {xiaosong.wang,yifan.peng,le.lu,luzh,mohammad.bagheri,rms}@nih.gov\
Download link: [Academic Torrents](http://academictorrents.com/details/e615d3aebce373f1dc8bd9d11064da55bdadede0)\
Download contributor(s): [Joseph Paul Cohen](http://academictorrents.com/userdetails.php?id=14), founder of Academic Torrents\

### Hálózat

#### ResNet - Deep Residual Learning for Image Recognition

Published: 2015-12-10\
Version: v1\
Contributor(s): Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun\
cs.CV: arXiv:1512.03385v1\
Paper: [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)\
Paper contributor(s): Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun\
Paper contact(s): {kahe, v-xiangz, v-shren, jiansun}@microsoft.com\
