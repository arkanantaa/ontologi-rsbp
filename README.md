# Dokumentasi Ontologi Pohon Keluarga

[cite_start]Dokumen ini merangkum semua komponen (TBox, ABox, dan Rules) yang didefinisikan dalam file `ontologi-keluarga.owx`.

## 1. TBox: Definisi Class

[cite_start]Hierarki Class utama didefinisikan di bawah `owl:Thing`[cite: 12]:
* [cite_start]**Person**[cite: 4]: Class dasar untuk semua individu.
    * [cite_start]**Deceased**: Sub-class dari `Person`, untuk individu yang sudah meninggal.
    * [cite_start]**Man**[cite: 2]: Sub-class dari `Person`.
    * [cite_start]**Parent**[cite: 2]: Sub-class dari `Person`, untuk individu yang memiliki anak.
    * [cite_start]**Woman**[cite: 5]: Sub-class dari `Person`.
* [cite_start]**Axioma Penting:** `Man` didefinisikan `DisjointWith` `Woman`[cite: 12].

---

## 2. TBox: Definisi Properties

Properti dibagi menjadi Data Properties (untuk literal) dan Object Properties (untuk relasi antar individu).

### Data Properties
* [cite_start]`hasAge` [cite: 7][cite_start]: (Domain: `Person`, Range: `xsd:int` [cite: 64]) - Usia individu, akan diisi oleh SWRL.
* [cite_start]`hasDOB` [cite: 7][cite_start]: (Domain: `Person`, Range: `xsd:int` [cite: 65]) - **(Sesuai Kompromi)** Tahun lahir individu.
* [cite_start]`hasDOD` [cite: 7][cite_start]: (Domain: `Person`, Range: `xsd:int` [cite: 65]) - **(Sesuai Kompromi)** Tahun kematian individu.
* [cite_start]`hasFirstName` [cite: 7][cite_start]: (Domain: `Person`, Range: `xsd:string` [cite: 65])
* [cite_start]`hasLastName` [cite: 7][cite_start]: (Domain: `Person`, Range: `xsd:string` [cite: 66])
* [cite_start]`hasMariageName` [cite: 7][cite_start]: (Domain: `Woman` [cite: 64][cite_start], Range: `xsd:string` [cite: 66]) - Akan diisi oleh SWRL.
* [cite_start]`hasSex` [cite: 8][cite_start]: (Domain: `Person`, Range: `xsd:string` [cite: 66])

### Object Properties (Ringkasan)
* **Relasi Inti (Manual):**
    * [cite_start]`hasSpouse` [cite: 6][cite_start]: (Karakteristik: `Symmetric` [cite: 52])
    * [cite_start]`hasChild` [cite: 3][cite_start]: (Domain: `Person` [cite: 53][cite_start], Range: `Person` [cite: 54])
* **Relasi Inversi (Otomatis):**
    * [cite_start]`hasParent` [cite: 5][cite_start]: (Karakteristik: `InverseOf hasChild` [cite: 52])
* **Sub-Properties (Otomatis):**
    * [cite_start]`hasSon` [cite: 6][cite_start]: (`SubPropertyOf hasChild` [cite: 51][cite_start], Range: `Man` [cite: 55])
    * [cite_start]`hasDaughter` [cite: 3][cite_start]: (`SubPropertyOf hasChild` [cite: 47][cite_start], Range: `Woman` [cite: 54])
    * [cite_start]`hasHusband` [cite: 4][cite_start]: (`SubPropertyOf hasSpouse` [cite: 49][cite_start], Range: `Man` [cite: 54])
    * [cite_start]`hasWife` [cite: 6][cite_start]: (`SubPropertyOf hasSpouse` [cite: 51][cite_start], Range: `Woman` [cite: 56])
    * [cite_start]`hasFather` [cite: 3][cite_start]: (`SubPropertyOf hasParent` [cite: 47][cite_start], Range: `Man` [cite: 54])
    * [cite_start]`hasMother` [cite: 4][cite_start]: (`SubPropertyOf hasParent` [cite: 49][cite_start], Range: `Woman` [cite: 55])
    * [cite_start]`hasBrother` [cite: 3][cite_start]: (`SubPropertyOf hasSibling` [cite: 47][cite_start], Range: `Man` [cite: 54])
    * [cite_start]`hasSister` [cite: 6][cite_start]: (`SubPropertyOf hasSibling` [cite: 51][cite_start], Range: `Woman` [cite: 55])
    * [cite_start]`hasOlderBrother` [cite: 5][cite_start]: (`SubPropertyOf hasBrother` [cite: 50])
    * [cite_start]`hasOlderSister` [cite: 5][cite_start]: (`SubPropertyOf hasSister` [cite: 50])
* **Relasi Rantai (Otomatis via Property Chain):**
    * [cite_start]`hasGrandParent`: `hasParent o hasParent` [cite: 58]
    * [cite_start]`hasGrandFather`: `hasParent o hasFather` [cite: 57]
    * [cite_start]`hasGrandMother`: `hasParent o hasMother` [cite: 57]
    * [cite_start]`hasParentInLaw`: `hasSpouse o hasParent` [cite: 62]
    * [cite_start]`hasFatherInLaw`: `hasSpouse o hasFather` [cite: 61]
    * [cite_start]`hasMotherInLaw`: `hasSpouse o hasMother` [cite: 62]
    * [cite_start]`hasUncle`: `hasParent o hasBrother` [cite: 56]
    * [cite_start]`hasAunt`: `hasParent o hasSister` [cite: 59]
    * [cite_start]`hasNiece`: `hasSibling o hasDaughter` [cite: 60]
    * [cite_start]`hasNephew`: `hasSibling o hasSon` [cite: 60]
    * [cite_start]`hasCousin`: `hasParent o hasSibling o hasChild` [cite: 59]

---

## 3. ABox: Input Individu dan Relasi Manual

[cite_start]Berikut adalah data manual (Asserted Axioms) yang harus dimasukkan untuk setiap individu[cite: 13, 14, 15, 16], disesuaikan dengan nama terakhir dari file XML Anda.

### Keluarga 1: Generasi 1
* [cite_start]**Dave** [cite: 8]
    * `hasFirstName`: "Dave"
    * [cite_start]`hasLastName`: "Smith" [cite: 27]
    * [cite_start]`hasSex`: "male" [cite: 27]
    * [cite_start]`hasDOB`: 1950 (integer) [cite: 27]
    * (Asserted Object Property)[cite_start]: `hasSpouse` -> `Hanna` [cite: 18]
    * (Asserted Object Property)[cite_start]: `hasChild` -> `Bob` [cite: 18]
* [cite_start]**Hanna** [cite: 8]
    * `hasFirstName`: "Hanna"
    * [cite_start]`hasLastName`: "Walker" [cite: 28] (Nama gadis)
    * [cite_start]`hasSex`: "female" [cite: 29]
    * [cite_start]`hasDOB`: 1952 (integer) [cite: 28]

### Keluarga 2: Generasi 1
* [cite_start]**Alan** [cite: 8]
    * [cite_start]`hasFirstName`: "Alan" [cite: 23]
    * `hasLastName`: "Woods"
    * [cite_start]`hasSex`: "male" [cite: 23]
    * [cite_start]`hasDOB`: 1950 (integer) [cite: 23]
    * (Asserted Object Property)[cite_start]: `hasSpouse` -> `Susan` [cite: 17]
    * (Asserted Object Property): `hasChild` -> `John` *(Harus ditambahkan manual)*
* [cite_start]**Susan** [cite: 10]
    * [cite_start]`hasFirstName`: "Susan" [cite: 42]
    * [cite_start]`hasLastName`: "King" [cite: 43] (Nama gadis)
    * [cite_start]`hasSex`: "female" [cite: 43]
    * [cite_start]`hasDOB`: 1951 (integer) [cite: 42]
    * [cite_start]`hasDOD`: 1990 (integer) [cite: 42]

### Keluarga Utama: Generasi 2
* [cite_start]**Bob** [cite: 8]
    * [cite_start]`hasFirstName`: "Bob" [cite: 26]
    * [cite_start]`hasLastName`: "Smith" [cite: 26]
    * [cite_start]`hasSex`: "male" [cite: 26]
    * [cite_start]`hasDOB`: 1975 (integer) [cite: 25]
    * (Asserted Object Property)[cite_start]: `hasSpouse` -> `Jane` [cite: 18]
* [cite_start]**Jane** (Istri Bob) [cite: 9]
    * [cite_start]`hasFirstName`: "Jane" [cite: 29]
    * [cite_start]`hasLastName`: "Baker" [cite: 30] (Nama gadis)
    * [cite_start]`hasSex`: "female" [cite: 30]
    * [cite_start]`hasDOB`: 1977 (integer) [cite: 29]
    * (Asserted Object Property): `hasChild` -> `Mary`, `Sue`, `Scott`, `Ann` *(Harus ditambahkan manual)*
* [cite_start]**John** (Anak Alan) [cite: 9]
    * [cite_start]`hasFirstName`: "John" [cite: 34]
    * [cite_start]`hasLastName`: "Woods" [cite: 34]
    * [cite_start]`hasSex`: "male" [cite: 35]
    * [cite_start]`hasDOB`: 1994 (integer) [cite: 34]
    * (Asserted Object Property)[cite_start]: `hasSpouse` -> `Mary` [cite: 20]
    * (Asserted Object Property)[cite_start]: `hasChild` -> `Tom`, `Jim` [cite: 19]

### Keluarga Utama: Generasi 3
* [cite_start]**Mary** (Anak Bob) [cite: 9]
    * [cite_start]`hasFirstName`: "Mary" [cite: 35]
    * [cite_start]`hasLastName`: "Smith" [cite: 36]
    * [cite_start]`hasSex`: "female" [cite: 36]
    * [cite_start]`hasDOB`: 1995 (integer) [cite: 35]
* [cite_start]**Sue** (Anak Bob) [cite: 10]
    * [cite_start]`hasFirstName`: "Sue" [cite: 41]
    * [cite_start]`hasLastName`: "Smith" [cite: 41]
    * [cite_start]`hasSex`: "female" [cite: 41]
    * [cite_start]`hasDOB`: 1997 (integer) [cite: 41]
* [cite_start]**Scott** (Anak Bob) [cite: 10]
    * [cite_start]`hasFirstName`: "Scott" [cite: 38]
    * [cite_start]`hasLastName`: "Smith" [cite: 38]
    * [cite_start]`hasSex`: "male" [cite: 39]
    * [cite_start]`hasDOB`: 1999 (integer) [cite: 38]
    * (Asserted Object Property): `hasSpouse` -> `Stephanie`
* [cite_start]**Ann** (Anak Bob) [cite: 8]
    * [cite_start]`hasFirstName`: "Ann" [cite: 24]
    * [cite_start]`hasLastName`: "Smith" [cite: 24]
    * [cite_start]`hasSex`: "female" [cite: 25]
    * [cite_start]`hasDOB`: 2001 (integer) [cite: 24]
* [cite_start]**Stephanie** (Istri Scott) [cite: 10]
    * [cite_start]`hasFirstName`: "Stephanie" [cite: 39]
    * [cite_start]`hasLastName`: "Parker" [cite: 40] (Nama gadis)
    * [cite_start]`hasSex`: "female" [cite: 40]
    * [cite_start]`hasDOB`: 2000 (integer) [cite: 39]
    * (Asserted Object Property): `hasChild` -> `Janice`, `Tommy`, `Sarah` *(Harus ditambahkan manual)*

### Keluarga Utama: Generasi 4
* [cite_start]**Tom** (Anak John) [cite: 10]
    * [cite_start]`hasFirstName`: "Tom" [cite: 44]
    * [cite_start]`hasLastName`: "Woods" [cite: 44]
    * [cite_start]`hasSex`: "male" [cite: 45]
    * [cite_start]`hasDOB`: 2020 (integer) [cite: 44]
* [cite_start]**Jim** (Anak John) [cite: 9]
    * [cite_start]`hasFirstName`: "Jim" [cite: 33]
    * [cite_start]`hasLastName`: "Woods" [cite: 33]
    * [cite_start]`hasSex`: "male" [cite: 33]
    * [cite_start]`hasDOB`: 2020 (integer) [cite: 32]
* [cite_start]**Janice** (Anak Scott) [cite: 9]
    * [cite_start]`hasFirstName`: "Janice" [cite: 31]
    * [cite_start]`hasLastName`: "Smith" [cite: 32]
    * [cite_start]`hasSex`: "female" [cite: 32]
    * [cite_start]`hasDOB`: 2020 (integer) [cite: 30]
    * [cite_start]`hasDOD`: 2021 (integer) [cite: 31]
* [cite_start]**Tommy** (Anak Scott) [cite: 10]
    * [cite_start]`hasFirstName`: "Tommy" [cite: 45]
    * [cite_start]`hasLastName`: "Smith" [cite: 46]
    * [cite_start]`hasSex`: "male" [cite: 46]
    * [cite_start]`hasDOB`: 2022 (integer) [cite: 45]
* [cite_start]**Sarah** (Anak Scott) [cite: 9]
    * [cite_start]`hasFirstName`: "Sarah" [cite: 37]
    * [cite_start]`hasLastName`: "Smith" [cite: 37]
    * [cite_start]`hasSex`: "female" [cite: 37]
    * [cite_start]`hasDOB`: 2024 (integer) [cite: 36]

---

## 4. Aturan SWRL (Dengan Koreksi)

Berikut adalah daftar lengkap aturan SWRL yang *seharusnya* ada di ontologi Anda, termasuk perbaikan kritis (ditandai **[KOREKSI]**) dan aturan yang hilang (ditandai **[TAMBAHAN]**) dari file XML Anda.

```prolog
// Rule 1: Man Classification [cite: 82]
Person(?p) ^ hasSex(?p, "male") -> Man(?p) [cite: 83, 84, 85]

// Rule 2: Woman Classification [cite: 79]
Person(?p) ^ hasSex(?p, "female") -> Woman(?p) [cite: 80, 81]

// Rule 3: Parent Classification [cite: 67]
Person(?p) ^ hasChild(?p, ?c) -> Parent(?p) [cite: 68, 69]

// Rule 4: Deceased Classification [cite: 75]
Person(?p) ^ hasDOD(?p, ?dod) -> Deceased(?p) [cite: 76, 77]

// Rule 5: Sibling Rule [cite: 97]
hasParent(?p, ?parent) ^ hasChild(?parent, ?s) ^ differentFrom(?p, ?s) -> hasSibling(?p, ?s) [cite: 98, 99, 100]

// Rule 6: Mariage Name Rule [cite: 86]
Woman(?w) ^ hasHusband(?w, ?h) ^ hasFirstName(?w, ?fn) ^ hasLastName(?h, ?ln) ^ swrlb:stringConcat(?mn, ?fn, " ", ?ln) -> hasMariageName(?w, ?mn) [cite: 87, 88, 89, 90, 91]

// Rule 7: Age Rule [KOREKSI]
// File XML Anda salah menggunakan hasAge di premis. Ini versi yang benar.
Person(?p) ^ hasDOB(?p, ?bYear) ^ swrlb:subtract(?age, 2025, ?bYear) -> hasAge(?p, ?age)

// Rule 8: Older Brother Rule [cite: 92]
hasBrother(?p, ?b) ^ hasDOB(?p, ?pDOB) ^ hasDOB(?b, ?bDOB) ^ swrlb:lessThan(?bDOB, ?pDOB) -> hasOlderBrother(?p, ?b) [cite: 93, 94, 95, 96]

// Rule 9: Older Sister Rule [KOREKSI]
// File XML Anda salah menyimpulkan hasSister. Ini versi yang benar.
hasSister(?p, ?s) ^ hasDOB(?p, ?pDOB) ^ hasDOB(?s, ?sDOB) ^ swrlb:lessThan(?sDOB, ?pDOB) -> hasOlderSister(?p, ?s)

// Rule 10a: Son Propagation Rule [cite: 111]
// Menyebarkan relasi 'hasSon' ke pasangan
hasSpouse(?p1, ?p2) ^ hasSon(?p1, ?c) -> hasSon(?p2, ?c) [cite: 112, 113]

// Rule 10b: Daughter Propagation Rule [cite: 102]
// Menyebarkan relasi 'hasDaughter' ke pasangan
hasSpouse(?p1, ?p2) ^ hasDaughter(?p1, ?c) -> hasDaughter(?p2, ?c) [cite: 103, 104]

// Rule 11: hasSon Inference Rule [TAMBAHAN]
// Aturan ini HILANG dari XML Anda. Ini penting untuk inferensi.
Person(?p) ^ hasChild(?p, ?c) ^ Man(?c) -> hasSon(?p, ?c)

// Rule 12: hasDaughter Inference Rule [TAMBAHAN]
// Aturan ini HILANG dari XML Anda. Ini penting untuk inferensi.
Person(?p) ^ hasChild(?p, ?c) ^ Woman(?c) -> hasDaughter(?p, ?c)