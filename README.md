# 🔐 Pcryption

Pcryption is a lightweight, pen-and-paper cipher designed to encrypt and decrypt text using nothing but a blank sheet of paper and a simple mathematical rotation. 

While it isn't designed to stop professional cryptanalysts, its main strength is its simplicity: **you do not need to carry a massive lookup table with you to use it.** If you understand the underlying pattern, you can encrypt and decrypt entirely from memory.

> ⚠️ **Disclaimer:** This project was created for fun and educational purposes. Do not use Pcryption to secure highly sensitive data!

---

## 🧭 How It Works (The Core Logic)

The cipher breaks down letters into a 3-digit code block following a strict mathematical rule. Every letter is assigned a code based on three columns that cycle sequentially (**Column 1 ➔ Column 2 ➔ Column 3 ➔ Column 1...**).

Each 3-digit code `[X][Y][Z]` is structured like this:
*   **`X` (The Group/Row):** Dictated by the column cycle. 
    *   Column 1 uses groups `1, 2, 3`
    *   Column 2 uses groups `4, 5, 6`
    *   Column 3 uses groups `7, 8, 9`
*   **`Y` (The Slot):** The specific position (`01` through `09`) inside that block.
*   **`Z` (The Global ID):** The raw position of the character in the global 81-character matrix.

Because of this layout, you can easily calculate the codes in your head without looking at the table below.

---

## 📊 The Cipher Matrix

| Column 1 (Cycle 1) | Column 2 (Cycle 2) | Column 3 (Cycle 3) |
| :--- | :--- | :--- |
| **101** A 1 | **401** A 28 | **701** A 55 |
| **102** B 2 | **402** B 29 | **702** B 56 |
| **103** C 3 | **403** C 30 | **703** C 57 |
| **104** D 4 | **404** D 31 | **704** D 58 |
| **105** E 5 | **405** E 32 | **705** E 59 |
| **106** F 6 | **406 F 33 | **706** F 60 |
| **107** G 7 | **407** G 34 | **707** G 61 |
| **108** H 8 | **408** H 35 | **708** H 62 |
| **109** I 9 | **409** I 36 | **709** I 63 |
| *---* | *---* | *---* |
| **201** J 10 | **501** J 37 | **801** J 64 |
| **202** K 11 | **502** K 38 | **802** K 65 |
| **203** L 12 | **503** L 39 | **803** L 66 |
| **204** M 13 | **504** M 40 | **804** M 67 |
| **205** N 14 | **505** N 41 | **805** N 68 |
| **206** O 15 | **506** O 42 | **806** O 69 |
| **207** P 16 | **507** P 43 | **807** P 70 |
| **208** Q 17 | **508** Q 44 | **808** Q 71 |
| **209** R 18 | **509** R 45 | **809** R 72 |
| *---* | *---* | *---* |
| **301** S 19 | **601** S 46 | **901** S 73 |
| **302** T 20 | **602** T 47 | **902** T 74 |
| **303** U 21 | **603** U 48 | **903** U 75 |
| **304** V 22 | **604** V 49 | **904** V 76 |
| **305** W 23 | **605** W 50 | **905** W 77 |
| **306** X 24 | **606** X 51 | **906** X 78 |
| **307** Y 25 | **607** Y 52 | **907** Y 79 |
| **308** Z 26 | **608** Z 53 | **908** Z 80 |
| **309** ␣ 27 *(Space)* | **609** ␣ 54 *(Space)* | **909** ␣ 81 *(Space)* |

---

## 📝 Step-by-Step Example

To encrypt a message, you shift columns for every single letter: **Column 1 ➔ Column 2 ➔ Column 3**, then restart at **Column 1**.

**Plaintext:** `Hello I am Chane`

### Cipher Shift Mapping:
```text
Letter:    H     e     l     l     o    [ ]    I     [ ]    C     h     a     n     e
Cycle:    (1)   (2)   (3)   (1)   (2)   (3)   (1)   (2)   (3)   (1)   (2)   (3)   (1)
Code:     108   405   803   203   506   909   401   609   103   408   701   205   405
