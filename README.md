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

## Reflection 2
![commit2](<Screenshot (683).png>)
Pada kode main.rs terdapat beberapa perubahan yang pertama yaitu menambahkan `fs` pada `use` statement. `fs` statement ini ditambahkan untuk membawa library filesystem ke dalam scope.
```
use std::{
    fs,
    io::{prelude::*, BufReader},
    net::{TcpListener, TcpStream},
};
```
Selain itu `let status_line = "HTTP/1.1 200 OK";` berfungsi  untuk menginisiasi respon HTTP dengan kode status 200 yang berarti respon berhasil. <br>
Line `fs::read_to_string("hello.html").unwrap();` akan membaca file hello.html. <br>
Line `let length = contents.len();` akan menyimpan panjang contents. Kemudian itu akan digabungkan menjadi satu response html pada `let response = format!("{status_line}\r\nContent-Length:{length}\r\n\r\n{contents}");`. Lalu repon akan dikirim kembali dengan line `stream.write_all(response.as_bytes()).unwrap();`. <br>
