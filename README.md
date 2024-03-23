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

## Reflection 3
![alt text](<Screenshot (684).png>)
Pada kode kali ini akan dibuat agar webserver dapat mereturn page error bila tidak ditemukan page yang sesuai. <br>

kode ini akan mengecek apakah `request_line` berisi GET request. Ketika kode status adalah 200, maka akan file hello.html akan dibaca dan dikembalikan. <br>

Apabila `request_line` tidak berisi GET request, maka akan masuk ke kondisi else, dimana kita akan menginisiasi `let status_line = "HTTP/1.1 404 NOT FOUND";` dan membaca file 404.html melalui kode `let contents = fs::read_to_string("404.html").unwrap();`.<br>


## Reflection 4
Pada commit ke-4 ini terdapat perubahan kode di bagian: 
```
    let (status_line, filename) = match &request_line[..] { 
        "GET / HTTP/1.1" => ("HTTP/1.1 200 OK", "hello.html"), 
        "GET /sleep HTTP/1.1" => { 
            thread::sleep(Duration::from_secs(10)); 
            ("HTTP/1.1 200 OK", "hello.html") 
        } 
        _ => ("HTTP/1.1 404 NOT FOUND", "404.html"), 
        };
```
Pada kode kali ini, ditambahkan kasus ketika client request `GET /sleep HTTP/1.1`. dengan ini, server akan sleep selama 10 detik sebelum repon ke hello.html.
