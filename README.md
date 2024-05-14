# Module 11 - Deployment on Kubernetes

> ##### Muhammad Daffa Grahito Triharsanto - 2206820075 - Pemrograman Lanjut B

## Hello Minikube

### Reflections
1. ***Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?***

    Dari log dapat dipahami bahwa sebelum meng*expose* aplikasinya sebagai service, aplikasinya diakses secara langsung di dalam pod. Log menunjukkan pesan-pesan awal (start server HTTP on port 8080) dan setiap permintaan masuk (GET /). Setiap kali aplikasi di access di dalam pod, dibuat entri log untuk request tersebut. Setelah menjadikan aplikasi sebagai service menggunakan `minikube service hello-node`, log tetap menunjukkan pesan-pesan awal dan permintaan masuk seperti sebelumnya namun sekarang aplikasi diakses melalui service, yang meneruskan traffic ke pod. Mengakses aplikasi melalui service memungkinkan akses eksternal ke aplikasi, sementara mengaksesnya di dalam pod lebih bersifat internal dalam cluster Kubernetes.
    ![Logs](assets/images/1.1.png)

2. ***Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?***

    Opsi `-n` dalam perintah `kubectl get` digunakan untuk menentukan namespace di mana resource akan ditampilkan. Jika tidak menyertakan opsi `-n`, `kubectl get` akan menampilkan resource dari namespace default. Pada pemanggilan yang kemudian, kubectl get digunakan dengan opsi `-n kube-system`, yang memberitahukannya untuk menampilkan resource dari namespace kube-system secara khusus. Namespace ini berisi system component dan infrastructure dari Kubernetes itu sendiri, seperti layanan inti sistem seperti DNS, server API, dan dashboard Kubernetes.