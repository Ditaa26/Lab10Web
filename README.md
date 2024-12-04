# Lab10Web
## Dita Tiara Putri
## 312310131
## TI 23 A1

# 1. Buat file baru dengan nama mobil.php 
![image](https://github.com/user-attachments/assets/5f8a621f-2182-4807-97e8-d7e8cd36e2dc)  
```sh
<?php
/**
* Program sederhana pendefinisian class dan pemanggilan class.
**/
class Mobil
{
    private $warna;
    private $merk;
    private $harga;

public function __construct()
{
    $this->warna = "Biru";
    $this->merk = "BMW";
    $this->harga = "10000000";
}
    public function gantiWarna ($warnaBaru)
    {
        $this->warna = $warnaBaru;
    }
    public function tampilWarna ()
    {
       echo "Warna mobilnya : " . $this->warna;
    }
}
// membuat objek mobil
$a = new Mobil();
$b = new Mobil();

// memanggil objek
echo "<b>Mobil pertama</b><br>";
$a->tampilWarna();
echo "<br>Mobil pertama ganti warna<br>";
$a->gantiWarna("Merah");
$a->tampilWarna();

// memanggil objek
echo "<br><b>Mobil kedua</b><br>";
$b->gantiWarna("Hijau");
$b->tampilWarna();

?>
```
![image](https://github.com/user-attachments/assets/9266e16a-62f3-4a34-ba53-92206931fe2f)  
Kode ini mendemonstrasikan penggunaan class dan objek di PHP untuk mengelola atribut mobil, seperti warna, dengan metode untuk menampilkan dan mengganti warnanya.  

# 2. Contoh class library untuk membuat form.
## Buat file baru dengan nama form.php.  
![image](https://github.com/user-attachments/assets/b7685eec-2c18-4ad7-a20a-6bd0491717fa) 
```sh
<?php
/**
* Nama Class: Form
* Deskripsi: Class untuk membuat form inputan text sederhana
**/
class Form
{
    private $fields = array();
    private $action;
    private $submit = "Submit Form";
    private $jumField = 0;

    public function __construct($action, $submit)
    {
        $this->action = $action;
        $this->submit = $submit;
    }

    public function displayForm()
    {
        echo "<form action='".$this->action."' method='POST'>";
        echo '<table width="100%" border="0">';
        for ($j = 0; $j < count($this->fields); $j++) {
            echo "<tr><td align='right'>".$this->fields[$j]['label']."</td>";
            echo "<td><input type='text' name='".$this->fields[$j]['name']."'></td></tr>";
        }
        echo "<tr><td colspan='2'>";
        echo "<input type='submit' value='".$this->submit."'></td></tr>";
        echo "</table>";
        echo "</form>";
    }

    public function addField($name, $label)
    {
        $this->fields[$this->jumField]['name'] = $name;
        $this->fields[$this->jumField]['label'] = $label;
        $this->jumField++;
    }
}

?>
```
ga muncul gambar apa apa karena, karena hanya berisi deklarasi class.

# 3. Contoh implementasi pemanggilan class library form.php 
## Buat file baru dengan nama form_input.php  
![image](https://github.com/user-attachments/assets/15752875-37aa-4713-825b-0f7716164652) 
```sh
<?php
/**
* Program memanfaatkan Program 10.2 untuk membuat form inputan sederhana.
**/
include "form.php";
echo "<html><head><title>Mahasiswa</title></head><body>";
$form = new Form("","Input Form");
$form->addField("txtnim", "Nim");
$form->addField("txtnama", "Nama");
$form->addField("txtalamat", "Alamat");
echo "<h3>Silahkan isi form berikut ini :</h3>";
$form->displayForm();
echo "</body></html>";
?>
```
![image](https://github.com/user-attachments/assets/da03e95d-b370-45ae-a5cd-96980b6a914d)  
Kode tersebut membuat form input sederhana untuk mengisi data mahasiswa (NIM, Nama, dan Alamat) dengan menggunakan kelas Form yang harus didefinisikan sebelumnya di file form.php.  

# 4. Contoh lainnya untuk database connection dan query. Buat file dengan nama database.php 
![image](https://github.com/user-attachments/assets/e99520ec-ba1a-41a4-bb00-88f2c9a3199a)  
```sh
<?php
class Database {
    protected $host;
    protected $user;
    protected $password;
    protected $db_name;
    protected $conn;

    public function __construct() {
        $this->getConfig();
        $this->conn = new mysqli($this->host, $this->user, $this->password, $this->db_name);

        if ($this->conn->connect_error) {
            die("Connection failed: " . $this->conn->connect_error);
        }
    }

    private function getConfig() {
        include_once("config.php");
        global $config; // Pastikan $config bisa diakses
        $this->host = $config['host'];
        $this->user = $config['username'];
        $this->password = $config['password'];
        $this->db_name = $config['db_name'];
    }

    public function query($sql) {
        $result = $this->conn->query($sql);
        if ($result === false) {
            die("SQL Error: " . $this->conn->error);
        }
        return $result;
    }

    public function get($table, $where = null) {
        $condition = $where ? " WHERE $where" : "";
        $sql = "SELECT * FROM $table$condition";
        $result = $this->query($sql);
        return $result->fetch_assoc();
    }

    public function insert($table, $data) {
        if (is_array($data)) {
            $columns = implode(", ", array_keys($data));
            $values = implode(", ", array_map(fn($val) => "'{$this->conn->real_escape_string($val)}'", $data));
            $sql = "INSERT INTO $table ($columns) VALUES ($values)";
            return $this->query($sql);
        }
        return false;
    }

    public function update($table, $data, $where) {
        if (is_array($data)) {
            $update_values = implode(", ", array_map(fn($key, $val) =>
                "$key='{$this->conn->real_escape_string($val)}'", array_keys($data), $data));
            $sql = "UPDATE $table SET $update_values WHERE $where";
            return $this->query($sql);
        }
        return false;
    }

    public function delete($table, $filter) {
        if (!empty($filter)) {
            $sql = "DELETE FROM $table WHERE $filter";
            return $this->query($sql);
        }
        return false;
    }
}
?>
```
## selanjutnya membuat table baru di database latihan1  
``` sh
MariaDB [(none)]> use latihan1;
Database changed
MariaDB [latihan1]> create table users (
    -> id INT AUTO_INCREMENT PRIMARY KEY,
    -> nama VARCHAR(30) NOT NULL,
    -> email VARCHAR(30) NOT NULL);
Query OK, 0 rows affected (0.016 sec)

MariaDB [latihan1]> INSERT INTO users (nama, email) VALUES
    -> ('dita tiara', 'dita26@gmail.com'),
    -> ('mica', 'mica09@gmail.com');
Query OK, 2 rows affected (0.095 sec)
Records: 2  Duplicates: 0  Warnings: 0
```
![image](https://github.com/user-attachments/assets/654cd4fa-fb9a-44a3-b4b4-0188e5d74225) 

## Lalu membuat file config.php
![image](https://github.com/user-attachments/assets/ab08c538-7911-437b-850e-5cc9175ccc3c) 
```sh
<?php
$config = [
    'host' => 'localhost',     
    'username' => 'root',      
    'password' => '',          
    'db_name' => 'latihan1'    
];
?>
``` 
## Lalu membuat file test.php
```sh
<?php
// Memasukkan file konfigurasi dan kelas Database
include_once 'config.php';
include_once 'database.php';

// Membuat objek Database dan menghubungkan ke database
try {
    $db = new Database();  // Membuat objek database
    echo "Koneksi ke database berhasil!<br>";
} catch (Exception $e) {
    echo "Koneksi gagal: " . $e->getMessage();
}

// Menguji operasi SELECT
$user = $db->get('users', 'id = 1');  // Mengambil data user dengan ID 1
if ($user) {
    echo "Data User ID 1: <br>";
    echo "Nama: " . $user['nama'] . "<br>";
    echo "Email: " . $user['email'] . "<br>";
} else {
    echo "User tidak ditemukan.<br>";
}

// Menguji operasi UPDATE
$updateData = [
    'nama' => 'Lala',
    'email' => 'lala32@gmail.com'
];
$updated = $db->update('users', $updateData, 'id = 1');
if ($updated) {
    echo "Data berhasil diperbarui!<br>";
} else {
    echo "Gagal memperbarui data.<br>";
}

// Menguji operasi DELETE
$deleted = $db->delete('users', 'id = 2');  
if ($deleted) {
    echo "Data berhasil dihapus!<br>";
} else {
    echo "Gagal menghapus data.<br>";
}
?>
```
![image](https://github.com/user-attachments/assets/f715fe4a-4729-4718-bc36-4fc788c53161)
![image](https://github.com/user-attachments/assets/2fd3f43b-8861-4efb-a535-9b34d50fab0d) 
Kode PHP ini berfungsi untuk menghubungkan aplikasi dengan database MariaDB menggunakan kelas Database, yang menangani operasi CRUD (Create, Read, Update, Delete). Pertama, kelas ini memuat konfigurasi database melalui file config.php dan membuat objek koneksi ke database latihan1 dengan menggunakan kredensial yang telah ditentukan. Setelah berhasil terkoneksi, kode ini menguji operasi SELECT untuk mengambil data pengguna dengan ID 1, operasi UPDATE untuk memperbarui nama dan email pengguna dengan ID 1, serta operasi DELETE untuk menghapus pengguna dengan ID 2. Hasil dari setiap operasi akan ditampilkan melalui pesan di browser, memberikan feedback mengenai keberhasilan atau kegagalan setiap operasi.  

# TUGAS 
Implementasikan konsep modularisasi pada kode program pada praktikum sebelumnya dengan menggunakan class library untuk form dan database connection.  















