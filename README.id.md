# rpg-character-generator

Modul Python ringan yang membangun lembar karakter RPG sederhana. Fungsi
`create_character` memvalidasi nama karakter dan tiga stat inti (strength,
intelligence, charisma), lalu mengembalikan lembar karakter yang diformat
dengan setiap stat digambar sebagai baris titik terisi dan kosong.

## Isi Folder

| Berkas          | Keterangan                                                    |
| --------------- | ------------------------------------------------------------- |
| `main.py`       | Mendefinisikan fungsi `create_character`.                     |
| `LICENSE`       | Dedikasi domain publik CC0 1.0 Universal.                     |
| `.gitignore`    | Aturan abaikan standar Python untuk version control.          |

## Cara Memulai

1. Pastikan Python 3 telah terpasang.
2. Impor dan panggil fungsi dari kode Anda sendiri:

   ```bash
   python -c "from main import create_character; print(create_character('Hero',3,2,2))"
   ```

## Cara Kerja

Modul menggunakan dua karakter penanda dan satu fungsi `create_character`:

```python
full_dot = '●'
empty_dot = '○'

def create_character(name, strength, intelligence, charisma):

    if type(name) is not str:
        return "The character name should be a string"
    if name == "":
        return "The character should have a name"
    if len(name) > 10:
        return "The character name is too long"
    if " " in name:
        return "The character name should not contain spaces"

    if type(strength) is not int or type(intelligence) is not int or type(charisma) is not int:
        return "All stats should be integers"

    if strength < 1 or intelligence < 1 or charisma < 1:
        return "All stats should be no less than 1"
    if strength > 4 or intelligence > 4 or charisma > 4:
        return "All stats should be no more than 4"

    if strength + intelligence + charisma != 7:
        return "The character should start with 7 points"

    str_line = f"STR {full_dot * strength}{empty_dot * (10 - strength)}"
    int_line = f"INT {full_dot * intelligence}{empty_dot * (10 - intelligence)}"
    cha_line = f"CHA {full_dot * charisma}{empty_dot * (10 - charisma)}"

    return f"{name}\n{str_line}\n{int_line}\n{cha_line}"
```

### Aturan Validasi

Sebelum membangun lembar, fungsi mengembalikan string kesalahan yang mudah
dipahami bila sebuah aturan dilanggar:

- `name` harus `str` → jika tidak `"The character name should be a string"`.
- `name` tidak boleh kosong → `"The character should have a name"`.
- `name` paling panjang 10 karakter → `"The character name is too long"`.
- `name` tidak boleh mengandung spasi →
  `"The character name should not contain spaces"`.
- `strength`, `intelligence`, dan `charisma` harus `int` →
  `"All stats should be integers"`.
- Setiap stat minimal `1` → `"All stats should be no less than 1"`.
- Setiap stat maksimal `4` → `"All stats should be no more than 4"`.
- Ketiga stat harus berjumlah tepat `7` →
  `"The character should start with 7 points"`.

Jika semua pemeriksaan lolos, setiap stat dirender sebagai `STR`/`INT`/`CHA`
diikuti `strength` titik terisi dan `10 - strength` titik kosong, menghasilkan
bar 10 sel per stat.

### Contoh Penggunaan

```python
from main import create_character

print(create_character("Hero", 3, 2, 2))
# Hero
# STR ●●●○○○○○○○
# INT ●●○○○○○○○○
# CHA ●●○○○○○○○○

print(create_character("A", 1, 1, 1))
# The character should start with 7 points
```

> Catatan: modul hanya mendefinisikan fungsi — tidak ada pemanggilan `print` di
> level atas, sehingga menjalankan `python main.py` tidak menghasilkan output.
> Imporlah seperti contoh di atas untuk menggunakannya.

## Konsep Utama

- Memvalidasi beberapa masukan dengan klausa penjaga (guard clauses) yang
  `return` lebih awal.
- Menggunakan `type(x) is not int` / `is not str` untuk pemeriksaan tipe ketat.
- Membangun string dengan f-string dan mengulang karakter dengan operator `*`.
- Mengembalikan hasil yang diformat atau pesan kesalahan yang jelas.

## Lisensi

Dirilis di bawah [CC0 1.0](LICENSE), menempatkan karya ini ke dalam domain
publik.
