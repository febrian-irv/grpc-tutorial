# Reflection

#### 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
a. Unary rpc merupakan communication protocol yang dimana client mengirimkan satu request pada server dan akan menerima satu response kemabali. Contoh scenario yang cocok adalah pengambilan data dari database.
b. Server streaming rpc adalah communication protocol dimana server akan mengirimkan responses secara terus menerus kepada client. Contoh scenario yang cocok adalah update-update informasi yang diperlukan secara real-time seperti cuaca.
c. Bidirectional streaeming adalah communication protocol yang dimana client dan server akan mengirimkan pesan satu sama lain secara terus menerus. Dengan itu, memberikan komunikasi dua arah yang real-time. Contoh scenario yang cocok adalah aplikasi chatting.

#### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
Adanya layered system yang memastikan komunikasi antar client dan server. Untuk autentikasi dipastikan adanya mekanisme autentikasi yang dapat diandalkan seperti JWT atau adanya two way authentication pada client dan juga server. Untuk autorisasi pastikan adanya batasan untuk gRPC method yang dapat dilakukan berdasarkan role dari client. Untuk enkripsi data pastikan terdapat transport layer yang memastikan kerahasiaan data dan memanfaatkan kriptografi untuk menciptakan keys dan secrets.

#### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
Pada kasus tersebut, dengan adanya aturan yang strict pada rust dalam melakukan concurrency maka perlu ketelatenan lebih dalam implementasi bidirectional streaming. Error handling seperti putusnya koneksi tidak terduga juga perlu diperhatikan karena merupakan dasar dari reliability komunikasi bidirectional. Salah satu keusulitan juga adalah bagaimana pada aplikasi chat dapat mengurutkan pesan sesuai waktunya dimana pesan diproses secara concurrently.

#### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Keuntungannya adalah fleksibilitas dalam memproses data stream sehingga dapat melakukan berbagai mekanisme komunikasi. Selain itu, kompatible dengan rust asynchronous model yang mempermudah mengintegrasikan dengan asynchronous  grpc service. Kesulitannya adalah kompleksitas pada kode yang mencampurkan asynchronous dengan concurrency. Error handling yang sulit dengan asynchronous programming serta fungsionalitas yang  mungkinterbatas akibat tidak secara langsung terhubung dengan gRPC.

#### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
Mendefine gRPC service terpisah dengan implementasi  yang menggunakan proto file sebagai service contract. Adanya seperation of concern dan layered structure yang membantu dalam testing dan maintenance. Melakukan enkapsulasi sesuai rust module system terkait fungsinalitas yang membantu keteraturan kode dan dapat digunakan kembali pada bermacam service.

#### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
Perlunya logic untuk memvalidasi dan autorisasi yang melakukan pembayaran karena pembayaran merupakan proses yang membutuhkan keamanan. Pembayaran juga perlu menghandle berbagai input sehingga terdapat penanganan data yang benar dan terhindar dari injection. Selain itu penggunaan autorisasi digunakan untuk memastikan client memiliki akses dan menghubungkan dengan payment gateway yang menghandle pembayaran tersebut.

#### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
gRPC menggunakan protobuf yang membantu mendefinisikan sevice contract diawal sehigga memudahkan untuk menegaskan batasan yang ada dan interoperabilty antara services yang ada. Dengan gRPC juga language neutral sehingga dapat diimplementasikan dengan berbagai bahasa dan arsitektur. Penggunaan HTTP/2 pada gRPC juga memberikan fitur yang membantu dalam komunikasi yang lebih efisien dan scalable dengan menurunkan latency dan memiliki throughput yang lebih baik.

#### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
Keuntungannya adalah multiplexing yang meberikan kemampuan komunikasi dikirim secara paralel pada satu koneksi, pengurangan ukuran http header, adanya kontrol pada transport layer untuk rate of data. Kesulitannya adalah infrastuktur lama yang belum tentu dapat mensupport http/2, penggunaan resource server yang lebih banyak, dankompleksitas pada http/2 yang lebih tinggi.

#### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
REST API menggunakan model request dan response dimana gRPC dapat melakukan pengiriman data secara concurrenly. Handling real-time pada grpc yang dapat dilakukan secara asinkronus tanpa model request response tidak seperti REST dimana client harus melakukan request terus menerus. Terdapat juga Server sent event pada REST yang memberikan kemampuan stream data dari server ke client namun dapat menyebabkan kenaikan latency.

#### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
Penggunaan grpc dengan skema dan rest api yang less skema menunjukkan bahwa dengan grpc proto dapat memberikan konsistensi implementasi pada berbagai komponen dan service. proto juga terdapat binary serializatin yang menyebabkan payload yang lebih kecil. proto juga mensuport backward compability terhadap evolusi skema dan terbalik pada rest yang kadan terdapat fitur yang tidak dapat diterima oleh teknologi yang lebih lama.