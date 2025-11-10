# Dokumentasi Ontologi Pohon Keluarga

## Kelompok 7:
1. Arkananta Masarief 5025231115
2. Rafi Faheem Aziz 5025231116
3. Kemal Tangguh Aji Rajasa 5025231263

## 1. TBox: Definisi Class

Hierarki Class utama didefinisikan di bawah `owl:Thing`:
* **Person**: Class dasar untuk semua individu.
    * **Deceased**: Sub-class dari `Person`, untuk individu yang sudah meninggal.
    * **Man**: Sub-class dari `Person`.
    * **Parent**: Sub-class dari `Person`, untuk individu yang memiliki anak.
    * **Woman**: Sub-class dari `Person`.
* **Axioma Penting:** `Man` didefinisikan `DisjointWith` `Woman`.

---

## 2. TBox: Definisi Properties

Properti dibagi menjadi Data Properties (untuk literal) dan Object Properties (untuk relasi antar individu).

### Data Properties
* `hasAge`: (Domain: `Person`, Range: `xsd:int`) - Usia individu, akan diisi oleh SWRL.
* `hasDOB`: (Domain: `Person`, Range: `xsd:int`) - **(Sesuai Kompromi)** Tahun lahir individu.
* `hasDOD`: (Domain: `Person`, Range: `xsd:int`) - **(Sesuai Kompromi)** Tahun kematian individu.
* `hasFirstName`: (Domain: `Person`, Range: `xsd:string`)
* `hasLastName`: (Domain: `Person`, Range: `xsd:string`)
* `hasMariageName`: (Domain: `Woman`, Range: `xsd:string`) - Akan diisi oleh SWRL.
* `hasSex`: (Domain: `Person`, Range: `xsd:string`)

### Object Properties (Ringkasan)
* **Relasi Inti (Manual):**
    * `hasSpouse`: (Karakteristik: `Symmetric`)
    * `hasChild`: (Domain: `Person`, Range: `Person`)
* **Relasi Inversi (Otomatis):**
    * `hasParent`: (Karakteristik: `InverseOf hasChild`)
* **Sub-Properties (Otomatis):**
    * `hasSon`: (`SubPropertyOf hasChild`, Range: `Man`)
    * `hasDaughter`: (`SubPropertyOf hasChild`, Range: `Woman`)
    * `hasHusband`: (`SubPropertyOf hasSpouse`, Range: `Man`)
    * `hasWife`: (`SubPropertyOf hasSpouse`, Range: `Woman`)
    * `hasFather`: (`SubPropertyOf hasParent`, Range: `Man`)
    * `hasMother`: (`SubPropertyOf hasParent`, Range: `Woman`)
    * `hasBrother`: (`SubPropertyOf hasSibling`, Range: `Man`)
    * `hasSister`: (`SubPropertyOf hasSibling`, Range: `Woman`)
    * `hasOlderBrother`: (`SubPropertyOf hasBrother`)
    * `hasOlderSister`: (`SubPropertyOf hasSister`)
* **Relasi Rantai (Otomatis via Property Chain):**
    * `hasGrandParent`: `hasParent o hasParent`
    * `hasGrandFather`: `hasParent o hasFather`
    * `hasGrandMother`: `hasParent o hasMother`
    * `hasParentInLaw`: `hasSpouse o hasParent`
    * `hasFatherInLaw`: `hasSpouse o hasFather`
    * `hasMotherInLaw`: `hasSpouse o hasMother`
    * `hasUncle`: `hasParent o hasBrother`
    * `hasAunt`: `hasParent o hasSister`
    * `hasNiece`: `hasSibling o hasDaughter`
    * `hasNephew`: `hasSibling o hasSon`
    * `hasCousin`: `hasParent o hasSibling o hasChild`

---

## 3. ABox: Input Individu dan Relasi Manual

Berikut adalah data manual (Asserted Axioms) yang harus dimasukkan untuk setiap individu, disesuaikan dengan nama terakhir dari file XML Anda.

### Keluarga 1: Generasi 1
* **Dave**
    * `hasFirstName`: "Dave"
    * `hasLastName`: "Smith"
    * `hasSex`: "male"
    * `hasDOB`: 1950 (integer)
    * (Asserted Object Property): `hasSpouse` -> `Hanna`
    * (Asserted Object Property): `hasChild` -> `Bob`
* **Hanna**
    * `hasFirstName`: "Hanna"
    * `hasLastName`: "Walker" (Nama gadis)
    * `hasSex`: "female"
    * `hasDOB`: 1952 (integer)

### Keluarga 2: Generasi 1
* **Alan**
    * `hasFirstName`: "Alan"
    * `hasLastName`: "Woods"
    * `hasSex`: "male"
    * `hasDOB`: 1950 (integer)
    * (Asserted Object Property): `hasSpouse` -> `Susan`
    * (Asserted Object Property): `hasChild` -> `John` *(Harus ditambahkan manual)*
* **Susan**
    * `hasFirstName`: "Susan"
    * `hasLastName`: "King" (Nama gadis)
    * `hasSex`: "female"
    * `hasDOB`: 1951 (integer)
    * `hasDOD`: 1990 (integer)

### Keluarga Utama: Generasi 2
* **Bob**
    * `hasFirstName`: "Bob"
    * `hasLastName`: "Smith"
    * `hasSex`: "male"
    * `hasDOB`: 1975 (integer)
    * (Asserted Object Property): `hasSpouse` -> `Jane`
* **Jane** (Istri Bob)
    * `hasFirstName`: "Jane"
    * `hasLastName`: "Baker" (Nama gadis)
    * `hasSex`: "female"
    * `hasDOB`: 1977 (integer)
    * (Asserted Object Property): `hasChild` -> `Mary`, `Sue`, `Scott`, `Ann` *(Harus ditambahkan manual)*
* **John** (Anak Alan)
    * `hasFirstName`: "John"
    * `hasLastName`: "Woods"
    * `hasSex`: "male"
    * `hasDOB`: 1994 (integer)
    * (Asserted Object Property): `hasSpouse` -> `Mary`
    * (Asserted Object Property): `hasChild` -> `Tom`, `Jim`

### Keluarga Utama: Generasi 3
* **Mary** (Anak Bob)
    * `hasFirstName`: "Mary"
    * `hasLastName`: "Smith"
    * `hasSex`: "female"
    * `hasDOB`: 1995 (integer)
* **Sue** (Anak Bob)
    * `hasFirstName`: "Sue"
    * `hasLastName`: "Smith"
    * `hasSex`: "female"
    * `hasDOB`: 1997 (integer)
* **Scott** (Anak Bob)
    * `hasFirstName`: "Scott"
    * `hasLastName`: "Smith"
    * `hasSex`: "male"
    * `hasDOB`: 1999 (integer)
    * (Asserted Object Property): `hasSpouse` -> `Stephanie`
* **Ann** (Anak Bob)
    * `hasFirstName`: "Ann"
    * `hasLastName`: "Smith"
    * `hasSex`: "female"
    * `hasDOB`: 2001 (integer)
* **Stephanie** (Istri Scott)
    * `hasFirstName`: "Stephanie"
    * `hasLastName`: "Parker" (Nama gadis)
    * `hasSex`: "female"
    * `hasDOB`: 2000 (integer)
    * (Asserted Object Property): `hasChild` -> `Janice`, `Tommy`, `Sarah` *(Harus ditambahkan manual)*

### Keluarga Utama: Generasi 4
* **Tom** (Anak John)
    * `hasFirstName`: "Tom"
    * `hasLastName`: "Woods"
    * `hasSex`: "male"
    * `hasDOB`: 2020 (integer)
* **Jim** (Anak John)
    * `hasFirstName`: "Jim"
    * `hasLastName`: "Woods"
    * `hasSex`: "male"
    * `hasDOB`: 2020 (integer)
* **Janice** (Anak Scott)
    * `hasFirstName`: "Janice"
    * `hasLastName`: "Smith"
    * `hasSex`: "female"
    * `hasDOB`: 2020 (integer)
    * `hasDOD`: 2021 (integer)
* **Tommy** (Anak Scott)
    * `hasFirstName`: "Tommy"
    * `hasLastName`: "Smith"
    * `hasSex`: "male"
    * `hasDOB`: 2022 (integer)
* **Sarah** (Anak Scott)
    * `hasFirstName`: "Sarah"
    * `hasLastName`: "Smith"
    * `hasSex`: "female"
    * `hasDOB`: 2024 (integer)

---

## 4. Aturan SWRL (Dengan Koreksi)

Berikut adalah daftar lengkap aturan SWRL yang ada di Ontologi

```prolog
// Rule 1: Man Classification
Person(?p) ^ hasSex(?p, "male") -> Man(?p)

// Rule 2: Woman Classification
Person(?p) ^ hasSex(?p, "female") -> Woman(?p)

// Rule 3: Parent Classification
Person(?p) ^ hasChild(?p, ?c) -> Parent(?p)

// Rule 4: Deceased Classification
Person(?p) ^ hasDOD(?p, ?dod) -> Deceased(?p)

// Rule 5: Sibling Rule (General)
hasParent(?p, ?parent) ^ hasChild(?parent, ?s) ^ differentFrom(?p, ?s) -> hasSibling(?p, ?s)

// Rule 6: Mariage Name Rule
Woman(?w) ^ hasHusband(?w, ?h) ^ hasFirstName(?w, ?fn) ^ hasLastName(?h, ?ln) ^ swrlb:stringConcat(?mn, ?fn, " ", ?ln) -> hasMariageName(?w, ?mn)

// Rule 7: Age Rule [KOREKSI]
Person(?p) ^ hasDOB(?p, ?bYear) ^ swrlb:subtract(?age, 2025, ?bYear) -> hasAge(?p, ?age)

// Rule 8: Older Brother Rule
hasBrother(?p, ?b) ^ hasDOB(?p, ?pDOB) ^ hasDOB(?b, ?bDOB) ^ swrlb:lessThan(?bDOB, ?pDOB) -> hasOlderBrother(?p, ?b)

// Rule 9: Older Sister Rule 
hasSister(?p, ?s) ^ hasDOB(?p, ?pDOB) ^ hasDOB(?s, ?sDOB) ^ swrlb:lessThan(?sDOB, ?pDOB) -> hasOlderSister(?p, ?s)

// Rule 10a: Son Propagation Rule
hasSpouse(?p1, ?p2) ^ hasSon(?p1, ?c) -> hasSon(?p2, ?c)

// Rule 10b: Daughter Propagation Rule
hasSpouse(?p1, ?p2) ^ hasDaughter(?p1, ?c) -> hasDaughter(?p2, ?c)

// Rule 11: hasSon Inference Rule
Person(?p) ^ hasChild(?p, ?c) ^ Man(?c) -> hasSon(?p, ?c)

// Rule 12: hasDaughter Inference Rule
Person(?p) ^ hasChild(?p, ?c) ^ Woman(?c) -> hasDaughter(?p, ?c)

// Rule 13: hasFather Inference Rule
Person(?p) ^ hasParent(?p, ?c) ^ Man(?c) -> hasFather(?p, ?c)

// Rule 14: hasMother Inference Rule
Person(?p) ^ hasParent(?p, ?c) ^ Woman(?c) -> hasMother(?p, ?c)

// Rule 15: hasBrother Inference Rule
Person(?p) ^ hasSibling(?p, ?s) ^ Man(?s) -> hasBrother(?p, ?s)

// Rule 16: hasSister Inference Rule
Person(?p) ^ hasSibling(?p, ?s) ^ Woman(?s) -> hasSister(?p, ?s)

// Rule 17: hasWife Inference 
Man(?p) ^ hasSpouse(?p, ?s) ^ Woman(?s) -> hasWife(?p, ?s)

// Rule 18: hasHusband Inference
Woman(?p) ^ hasSpouse(?p, ?s) ^ Man(?s) -> hasHusband(?p, ?s)
