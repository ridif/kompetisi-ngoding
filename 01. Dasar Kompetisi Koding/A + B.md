# A + B

| Nama 					| Nilai        	|
| ------------- | ------------- |
| Input file:   | aplusb.in     |
| Output file:  | aplusb.out 		|
| Time limit:   | 2 seconds 		|
| Memory limit: | 256 megabytes |

Diberikan dua nilai bertipe integer, A dan B. Output yang dihasilkan adalah A + B

### Input
File input mengandung satu baris dengan 2 nilai integer, A dan B (-10<sup>9</sup> <= A, B <= 10<sup>9</sup>), dipisahkan dengan satu spasi

### Output
Output berupa satu baris hasil dari A + B di file output.

### Contoh
| aplusb.in			| aplusb.out   	|
| ------------- | ------------- |
| 23 11					| 34						|

### Solusi
Problem ini sangat sederhana: hanya **tambahkan dua bilangan dan cetak hasilnya.**

Namun, kamu perlu mengetahui atau belajar bagaimana cara membuka file, membaca integer dari file, dan menuliskannya ke dalam file pada bahasa pemrograman pilihanmu. Seperti yang sudah disampaikan pada README.md di main tree, bahwa solusi yang diberikan hanya dalam bahasa C++ dan Java. Namun saya yakin kalian bisa mengubah ke bahasa lain berdasarkan analisa solusi.

#### C++, maximum time: 15 ms, maximum memory: 2308 kb.
Solusi ini menunjukkan bagaimana menggunakan input/output yang digunakan khusus pada C++
std::ifstream dan std::ofstream

```cpp
#ifdef JUDGE
#include <fstream>
std::ifstream cin("aplusb.in");
std::ofstream cout("aplusb.out");
#else
#include <iostream>
using std::cin;
using std::cout;
#endif

int main() {
	int a, b;
	cin >> a >> b;
	cout << a + b;
	return 0;
}
```

#### Java, maximum time: 125 ms, maximum memory: 17856 kb.
Solusi dengan Java ini menggunakan ```java.io.BufferedReader``` untuk membaca file. Class ini dapat membaca baris, dan itulah bagian menariknya. Class ini cukup cepat dalam konteks praktikal. Faktanya, ```BufferedReader``` jauh lebih cepat prosesnya daripada class ```Scanner```, 125ms:171ms untuk kasus sederhana. Perbedaan ini sangat signifikan jika kasus lebih kompleks. Hal ini karena ```Scanner``` menggunakan regular expression untuk parsing input, dan sangat terlihat pada saat running time. Pada solusi ini juga digunakan java.util.StringTokenizer untuk split baris ke bagian-bagian. Cara ini lebih ideal untuk digunakan.

```java
import java.io.*;
import java.util.*;

public class Main {
	static BufferedReader newInput() throws IOException {
		if (System.getProperty("JUDGE") != null) {
			return new BufferedReader(new FileReader("aplusb.in");
		} else {
			return new BufferedReader(new InputStreamReader(System.in));
		}
	}

	static PrintWriter newOutput() throws IOException {
		if (System.getProperty("JUDGE") != null) {
			return new PrintWriter("aplusb.out");
		} else {
			return new PrintWriter(System.out);
		}
	}
	public static void main(String[] args) throws IOException {
		try (BufferedReader in = newInput(); PrintWriter out = newOutput()) {
			StringTokenizer tok = new StringTokenizer(in.readLine());
			int a = Integer.parseInt(tok.nextToken());
			int b = Integer.parseInt(tok.nextToken());
			out.println(a + b);
		}
	}
}
```
