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

// Membuat objek Form
$form = new Form("proses.php", "Kirim Data");

// Menambahkan field ke form
$form->addField("nama", "Nama");
$form->addField("email", "Email");

// Menampilkan form
$form->displayForm();
?>
```
![image](https://github.com/user-attachments/assets/757c8e16-1750-449b-a94c-61bf06cf7fa4) 
Kode ini mendemonstrasikan pembuatan form dinamis menggunakan class di PHP, yang memungkinkan penambahan field input dan pengiriman data melalui metode POST.  

# 3. Contoh implementasi pemanggilan class library form.php 
## Buat file baru dengan nama form_input.php  
![image](https://github.com/user-attachments/assets/15752875-37aa-4713-825b-0f7716164652) 








