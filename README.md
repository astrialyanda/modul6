## Reflection 1
function handle_connection akan membaca data dari TCP stream dan meng-print-nya sehingga data dapat kita lihat dikirim dari browser. <br>

di function handle_connection, terdapat instance BufReader yang akan membungkus reference mutable ke stream. <br>

```
let buf_reader = BufReader::new(&mut stream); 
```

Variabel `http_request` akan mengumpulkan barisan request yang dikirim oleh browser ke server kita. Kita menambahkan vector Vec<_> untuk menandakan bahwa kita ingin mengumpulkan baris-baris request tersebut. <br>
```
let http_request: Vec<_> = buf_reader
```