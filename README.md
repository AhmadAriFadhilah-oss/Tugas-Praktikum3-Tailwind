### 1. Jelaskan keputusan `grid-cols/gap` di tiap *breakpoint* — kenapa begitu?

Keputusan ini diambil berdasarkan logika **tampilan paling optimal** di setiap perangkat, mirip dengan Instagram aslinya.

* **Default (`grid-cols-1`)**: Untuk *mobile* (`<640px`). Di layar HP, **satu kolom** adalah pilihan terbaik karena memaksimalkan visibilitas gambar. *Gap* yang sedikit membuat konten tidak terlalu padat.
* **`sm:grid-cols-2` (`>640px`)**: Transisi untuk tampilan tablet kecil atau *landscape* *mobile*. Dua kolom adalah *sweet spot* agar konten tidak terlalu besar, tapi juga tidak terlalu kecil.
* **`lg:grid-cols-3` (`>1024px`)**: Untuk *desktop* dan laptop. **Tiga kolom** adalah tampilan standar yang kita kenal di Instagram. Ini memaksimalkan ruang layar tanpa membuat gambar terlalu kecil, sehingga *user* bisa melihat banyak postingan sekaligus.
* **`gap-4`**: Digunakan untuk memberi jarak antar *grid item*. Angka `4` (sekitar `1rem` atau `16px`) ini adalah pilihan yang pas. Tidak terlalu rapat sehingga mata lelah, tidak terlalu jauh sehingga *layout* terlihat terpisah-pisah.

### 2. Bagaimana kamu memanfaatkan *utility responsive* Tailwind untuk memecahkan masalah *layout* yang muncul di *mobile*?

Pendekatan **Mobile-First** adalah kuncinya. Saya mulai dengan `grid-cols-1` di *breakpoint* terkecil. Setelah itu, saya "menambahkan" aturan baru untuk *breakpoint* yang lebih besar menggunakan prefiks seperti `sm:` dan `lg:`.

Contohnya, untuk tombol `Follow/Edit Profile`, di *mobile* saya membuatnya **berbaris vertikal** agar mudah dijangkau dengan `flex-col` atau `flex-wrap`. Lalu, untuk *breakpoint* yang lebih besar, saya tinggal menimpanya (`override`) dengan kelas `flex-row` untuk membuatnya sejajar horizontal. Ini memecahkan masalah tombol yang terlalu kecil atau tumpang tindih di *mobile*.

Dengan pendekatan ini, saya tidak perlu lagi menulis banyak `media query` kustom. Semua logika responsif sudah tertanam dalam nama kelasnya, membuat kode lebih ringkas dan mudah dibaca.

### 3. Jelaskan *trade-off* antara memakai banyak *utility classes* vs membuat *component* CSS tersendiri.

Ini pertanyaan favorit! Keduanya punya kelebihan dan kekurangan, tergantung kebutuhan proyek.

**Memakai banyak *utility classes* (seperti di proyek ini):**

* **Kelebihan:**
    * **Cepat & Ringkas:** Sangat cepat untuk *prototyping* atau proyek kecil. Kita tinggal ketik kelas di HTML, dan `layout` langsung jadi.
    * **Tidak Perlu Ganti File:** Tidak perlu bolak-balik antara HTML dan CSS. Semua *styling* ada di satu tempat.
    * **Mudah Dibaca:** Setelah terbiasa, kita bisa tahu gaya suatu elemen hanya dari melihat *class*-nya.

* **Kekurangan:**
    * **HTML Jadi Penuh (Terlalu Verbose):** Untuk elemen yang sama, kelas yang berulang-ulang akan membuat kode HTML sangat panjang dan sulit dibaca. Contohnya, jika ada 100 tombol yang sama, kita harus menulis kelas `bg-blue-500 text-white px-4 py-2 rounded-lg` sebanyak 100 kali.
    * **Sulit Mengubah Skala Besar:** Jika di tengah jalan kita ingin mengubah warna utama dari biru menjadi merah, kita harus mengubah setiap *class* `bg-blue-500` satu per satu.

**Membuat *component* CSS tersendiri (dengan `@apply` atau SCSS):**

* **Kelebihan:**
    * **Kode Bersih & Mudah Dirawat:** HTML tetap bersih, misalnya hanya `<button class="btn-primary">`.
    * **Mudah Diubah Skala Besar:** Jika warna utama ingin diubah, cukup ganti satu baris kode di *file* CSS komponen (`.btn-primary`), dan semua tombol akan otomatis berubah.
    * **Reusable:** Komponen bisa dipakai di mana saja di seluruh proyek.

* **Kekurangan:**
    * **Butuh Waktu Setup:** Membutuhkan waktu ekstra untuk membuat struktur folder CSS dan mendefinisikan setiap kelas komponen.
    * **Perlu Bolak-Balik File:** Mengubah *styling* butuh pindah dari *file* HTML ke *file* CSS.

**Kesimpulan:** Untuk proyek kecil seperti ini, **menggunakan banyak *utility classes* adalah pilihan terbaik** karena sangat cepat dan efisien. Namun, untuk proyek skala besar di mana konsistensi desain sangat penting, **membuat *component* CSS terpisah** (menggunakan `@apply`) akan jauh lebih logis dan mudah dirawat.

---
